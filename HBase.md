## 分布式数据库Hadoop Database(HBase) ##
1. BigTable基于GFS实现，HBase基于HDFS实现
特点：**列存储**、**可伸缩**、**实时读写**、**分布式**、**高性能高可靠**；存储非结构化数据，基于列而非行，是**非关系型数据库** 如(Cassandra/HBase/MongoDB/Neo4j)
2. 基于HDFS，利用MapReduce处理HBase中的海量数据，用zookeeper做分布式协同服务
3. 主要用来存储非结构化或半结构化的松散数据(列存储NoSQL数据库)
4. 区别于Hive数据仓库，HBase本身就是一个数据库

结构：Master/Slave架构，主节点HMaster，从节点为HRegionServer。

> HMaster是由zookeeper的选举机制选出的唯一管理节点。HMaster通过zookeeper分配协调HRegionServer崩溃时的Regions，HBaseClient也是通过zookeeper，得到HMaster、HRegionServer、-ROOT-核心数据之后，才能访问HRegionServer

![](https://uploadfiles.nowcoder.com/images/20190524/4206388_1558706443205_D3529FCA4176D9B2F36EADAC74ABA0C4)

## HBase和关系数据库的差别 ##
1. HBase仅提供文本类型数据，其他的自行处理
2. 不支持表之间的关联操作查询
3. 列式存储，CF由若干个文件保存
4. 修改和删除实际上是插入了新的带特殊标志的记录，保存有多个版本。在StoreFile进行合并的时候进行数据更新，而不是直接覆盖
5. 支持分布式，实现高性能数据增长
6. 不必先定义可随时插入新的限定符

## HBase数据模型 ##
1. rowkey/timestamp/CF1(列族)/CF2/CF3
2. 定义表的时候需要声明列族，列是在插入数据的时候声明
3. 版本由timestamp决定是高或低，低版本的记录不会被删掉，合并的时候会被删除；版本覆盖解决数据更新的问题，保留多版本号，可以查询到历史
4. CF2:q1 = val1 由rowkey+cf+q1即可确定到一个cell数据

### rowkey ###
1. 决定一行记录/按照字典序排序/只能存储64k的字节数据
2. rowkey的设计很关键，对实时查询
3. 设计的时候一般会加“业务字段”+“时间戳”，先按照业务字段排序，再按照时间戳排序
4. 若最新的时间排在上面，就拿MAX-time，最新时间就排在靠前

### ColumnFamily列族&Qualifier限定符 ###
1. CF是处理的最小单位，处理的时候可以没有列，但是一定要有CF。定义表模式(Table Schema)的时候必须预先指出CF的定义。如create ‘test’, 'course'
2. 每个q都归属于某一个CF，且可以动态按需在CF下加入新的q。CF下的列成员表示方法为
	
		course:math,course:english
3. 权限控制、存储和调优都是在CF的层面进行的
同一CF下的数据存储在同意目录下，由几个文件保存

### timestamp 时间戳(版本号)###
1. 版本控制，区别cell下的数据版本。按照时间倒序排列，最新的在最前
64位整型数据

### cell ###
1. 行列坐标交叉决定。有版本区分，即保存着不同版本的数据。
2. cell中是未解析的**字节数组**，以字节码的形式存储，不需要数据类型定义。
3. 唯一确定：{rowkey,column(<cf>+<q>,version)} => cell

### HLog ###
1. 普通的Hadoop Sequence File。有**操作日志**和操作的**数据信息**。
2. HLog的Key是HLogKey对象，其中记录了写入数据的归属信息，包括table和region的名字，还有sequence number和timestamp
3. HLog的Value是HBase的KeyValue对象，对应HFile中的KeyValue

### 物理模型 ###
1. 物理模型实际上，把概念模型中的一个行分割，并按照列进行存储。其中空值不会被存储，未指明时间戳就返回最新的版本。
2. 按照rowkey进行分割，按照CF进行存储

## Region ##
1. HBase分布式存储和负载均衡的最小单位。可以是Table划分出来的Region，也可以是.META.表划分出来的Region。
一个HRegionServer管理维护多个Regions实例HRegion，但是一个Region只存在于一个RegionServer，物理上存在于HDFS。HRegionServer还负责维护HLog。记录着管理的所有Regions的操作日志
2. HLog是用来做灾难备份的，采用预写式日志WAL(Write-Ahead Log)。一个HRegionServer对应着一个HLog，因此HLog中记录着所有HRS管理的所有的Region，避免对多个文件读写减少了寻址次数提高性能。一个HRS故障之后需要HMaster对HLog进行拆分，然后对Region进行重新分配。
3. 每个Region由若干个Store组成。**一个Store对应一个列族下的所有数据**。一个Store只有一个MemStore，用来缓存数据，缓存到一定数量的时候就持久化到本地变为StoreFile，因此SF可以有多个，但MS只有一个。其中SF是以HFile的格式存储于HDFS之中。(HFile是针对于HDFS来讲的，StoreFile是针对于HBase来说，其实HFile = StoreFile)

![](https://uploadfiles.nowcoder.com/images/20190524/4206388_1558706458776_30D3AF1CE259BA1F0F2E8E421B1D3E54)

## HBase写操作 ##
1. HClient先通过Zookeeper(得到HMaster、HRegionServer、-ROOT-核心数据)，找到需要访问的HRegionServer
2. 和HRegionServer建立连接，向Region提交变更，写入WAL日志和MemStore中
3. 当MS达到阈值1之后，启动单独的线程持久化为SF，SF文件足够多高于阈值2的时候就合并(Compact)成一个SF，当单个的SF文件足够大高于阈值3的时候就对当前的Region进行拆分(Split)成两个Regions，并由HM分发到其他的HRS中实现负载均衡。
4. 在Compact的过程中会对SF进行版本合并和数据删除，即HBase会一直增加数据，只有在合并的过程中才会进行更新和删除操作。HDFS不擅长于小文件处理，合并过程中会解决数据倾斜？
5. Compact分为minor和major两种合并方式。minor自动触发，少量的小文件进行简单的合并；major是人工出发，用于大量的StoreFile合并为很大的SF，同时在合并的过程中，根据数据的失效标记，对版本进行更新，对数据进行删除

## HMaster作用 ##
1. 将Regions分配给HMS&协调HMS之间的负载&维护集群的状态
2. 通过zookeeper感知发生故障的HMS，获取并处理其对应的HLog，将故障的Regions重新分配
3. 负责管理表的Schema和对元数据的操作，用户对Table的增删改查操作

## HRegionServer作用 ##
1. 相应用户的I/O请求，向HDFS中读写文件
2. 管理多个HRegion对象
3. HRegion中的StoreFile过大时进行Split操作生成两个新的Regions，父Region下线，新的Regions被HM分到HRegionServer中

> HRS和HClient建立连接之后，HRS会创建对应的HRegion实例，HRegion会为每个表的HCF建立一个Store实例
> 
> Store中包含一个HLog、一个MemStore和若干个StoreFile，StoreFile合并为大的SF再被拆分为Regions，被HM分发；
> 
> MemStore是和HLog结合使用的，源自WAL的预习机制。日志没有写到WAL中时，HRS崩溃可以回滚到写日志之前；一旦写入WAL，数据就会写入内存MemStore中，检验MS大小，足够大的时候就作为StoreFile写入到硬盘

![](https://uploadfiles.nowcoder.com/images/20190525/4206388_1558794527381_985F1362C55C9E5953811D171D935C3F)

## 元数据表 ##
1. 用户表的Regions的元数据存储于.META.表中，随着Regions变多，记录Regions的元数据的.META.表也变大，因此.META.表也需要分裂成多个Regions。
2. .META.的Regions的元数据又保存于-ROOT-表(不可再分，可以理解为只有一个Region)中，zookeeper记录-ROOT-表的位置


	//HClient最多三次就能找到Regions了
	HClient=>zookeeper=>-ROOT-=>.META.=>Regions
> 其中为了提高访问速度，.META.表的Region全都保存在内存中。

1. 客户端访问Regions之前会先查看本地的缓存。缓存包括-ROOT-、.META.表和Regions的位置信息。
2. 没有缓存就询问有Regions元数据的.META.表所在的HRegionServer
3. .META.表也没查到就找有.META.表元数据Region的-ROOT-表，从而找到.META.继而找到Regions
4. 若前面的信息全部**失效**就通过zookeeper重新定位-ROOT-、.META.表以及Regions的位置信息。此时需要进行6次网络来回才能定位到Regions(信息为空的时候，需要3次缓存更新；信息失效会先需要3次网络来回，验证信息确实失效，然后再有3次更新信息缓存，3+3=6)
5. HBase能提供**实时计算服务**主要原因是由其架构和底层的数据结构决定的，即由LSM-Tree(Log-Structured Merge-Tree) + HTable(region分区) + Cache决定——客户端可以直接定位到要查数据所在的HRegion server服务器，然后直接在服务器的一个region上查找要匹配的数据，并且这些数据部分是经过cache缓存的


![](https://uploadfiles.nowcoder.com/images/20190524/4206388_1558706472244_73AC7C87A9A6D2EB3C6C3DEB988F62B4)

## HBase索引 ##
1. 行转列列转行即可√
2. 对于经常查询的Qualifier，将限定符的取值范围作为rowkey，而原来的行键作为列构建新的表，即可实现根据列值快速定位数据所在行，即索引。
3. 索引表只包含一个列

## HClient ##
访问HBase的接口，维护cache加快对HBase的访问

## zookeeper ##
分布式协作服务
1. 用来存储-ROOT-表的地址、HMaster的地址和HRegionServer的地址。存储着所有Regions的地址；存储着HBase的schema和table元数据，Hive将元数据存储在关系数据库中，HBase存在ZK中
2. HM通过ZK感知HRS的状态，监控HRS的上下线信息并实时通知HM
3. HBase中可以启动多个HMaster，但是ZK的选举机制保证集群中只有一个HM为当前集群的master
4. 当HM出现单点故障，会立即选出一个新HM的作为master

### HA配置 ###

> 解压安装，加环境变量
> 
> /conf/zoo.cfg 指定datadir目录
> 
> server.1(serverid)=192.168.213.141:2888(有leader):3888(无主选leader用)
> 
> server.2=192.168.213.142:2888:3888
> leader(单点)&follower(推选)：优先事务id，次要serverid
> 
> datadir下加myid文件  追加serverid

![](https://uploadfiles.nowcoder.com/images/20190529/4206388_1559142686932_2D58A1A8ECC9672B25A230C50E0F8963)


hadoop在HA模式下secNameNode就没用了
hdfs-site.xml 逻辑物理映射，ZKFC
core-site.xml 逻辑名称为定义的字符串名称，zookeeper列表zoo.cfg & myid

## Sqoop ##
关系数据ETL工具，HDFS<->关系数据库

## Flume ##
日志收集工具