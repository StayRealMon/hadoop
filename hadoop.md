## Hadoop安装流程 ##
1. jdk1.8环境安装&环境变量配置
2. ssh免密配置ssh-keygen -t -rsa ？
3. 配置hostname，测试免密
4. hadoop2.7 压缩包安装
5. /etc/hadoop/关键配置文件(core-site.xml&hdfs-site.xml&mapred-site.xml&yarn-site.xml)
5.1 core-site	hdfs://master:9000&hadoop.tmp.dir
5.2 hdfs-site	NN.dir&DN.dir
5.3 mapred-site	framework->yarn
5.4 yarn-site	RMwebappaddr->master:8088&RMaddr&minmaxallocation
6. hdfs -format①②③④

## HDFS ##
1. HDFS的设计目的是为了支持Map-Reduce分布式计算框架，其次才是一个文件系统，FileSystem不是重点。
2. 特点
> 低廉的节点和硬盘存储，导致错误是常态，且冗余较高
> 目的是为了大数据分析而不是事务处理。因此适用于流式访问和批处理，不支持随机读取而是一写多读
> 数据在节点之间有距离的概念。优先寻找本机数据，其次是就近机架的数据。
> 优点：①高容错多副本自恢复②批处理&移动分布计算(计算向数据移动)&block位置暴露给计算框架，计算框架自行读取文件③大数据PB级百万文件万级节点④廉价可靠&容灾恢复
> 缺点：①不适用于低延迟高吞吐②小文件存取时占内存，寻找时间大于读写时间③不支持并发写入和随机修改，同一时间仅仅支持一个写操作，文件修改仅仅支持append
3. 文件在HDFS中是以块 Block 为单位存储的。默认64M，备份*3

## OLTP与OLAP ##
数据处理大致可以分成两大类：联机事务处理OLTP（on-line transaction processing）、联机分析处理OLAP（On-Line Analytical Processing）。
> OLTP是传统的关系型数据库的主要应用，主要是基本的、日常的事务处理，例如银行交易。
> OLAP是数据仓库系统的主要应用，支持复杂的分析操作，侧重决策支持，并且提供直观易懂的查询结果。 
> OLTP 系统强调数据库内存效率，强调内存各种指标的命令率，强调绑定变量，强调并发操作；
> OLAP 系统则强调数据分析，强调SQL执行市场，强调磁盘I/O，强调分区等

## Name Node ##
Name Node作用：
> ①管理文件sys的命名空间
> ②Block在DN上的位置和备份位置。通过心跳，DN宕机时抽空复制，备份过少进入安全模式(刚启动时有安全模式是因为还有节点没有汇报心跳，几分钟后收到心跳就可以解除安全模式了)
> ③事务日志edit_log和快照文件fsimage
> ④与client进行通信

NN所维护的信息：元数据信息(文件的时间大小权限所有者等)；**DN**的位置和状态；**Block**的位置和状态；维护虚拟的目录树；
NN的**Block块信息来自于DN的心跳汇报**
NN维护的信息基于内存，存在**单点故障**问题。通过保存edit_log&fsimage到disk以实现**持久化**
SecNN首次备份从NN获取edit_log和fsimage(两个文件都需要)，以后只获取edit_log即可。
> SecNN先停用NN的edit_log，NN先将新的log存至edit_log_new
> SecNN合并拿来的edit_log和**本地的fsimage**为新的fsimage并返回新的fsimage给NN
> NN将edit_log_new重命名为edit_log

首次format后启动NN时，生成空白fsimage，执行edit_log
> 若NN的内存满了就不能进行读写新建元数据，NN是集群的约束瓶颈
> fsimage中不保存Block的位置信息和DN的位置和状态，来自于DN的心跳汇报

## Data Node ##
Data Node作用：①对本节点进行管理②提交自己保存的Block列表。**一写多读**，向NN心跳汇报状态
> 文件线性切割成块(Block)以字节为单位，有**偏移量**(offset)和**位置信息**。块的第一个字节面向于源文件的下标即为偏移量
> Block的大小需要考虑硬盘的I/O量
> disk负责保存实际的Block，以及描述Block的元数据信息(一个md5校验小文件)

## Block的副本放置策略 ##
1. 第一块副本放在上传文件的DN，磁盘不太满，CPU不太忙的节点
2. 和第一个副本放在不同机架的节点上
3. 与第二个副本相同的机架节点上
4. 更多的节点随机放

## HDFS写流程 ##
1. client访问NN，NN如果说有此文件就不能写了。若没有文件，创建filename_copying
2. NN按照副本放置策略找到三个或多个节点返回DN List
3. client仅仅与DN List中的第一个节点DN1进行socket连接(副本透明，给DN1传输成功完成就ok)，将64M的Block切割为更小的packet，利用时间线重叠，行成pipeline进行流式传输
4. NN根据DN List的心跳汇报校验Block的位置，将filename返回
> 若有节点挂掉，根据本身的副本数量汇报进行复制，保证数量高于安全模式的阈值
> 若全部挂掉，返回写失败

## HDFS读流程 ##
1. client访问NN寻求文件
2. NN根据本身维护的Block位置信息，对节点进行排序(根据副本放置策略)，返回给client
3. client从DN List中排序级别较高**距离最近**的节点读取对应的块

## MapReduce ##