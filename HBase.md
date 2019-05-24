## 分布式数据库HBase ##
BigTable基于GFS实现，HBase基于HDFS实现
特点：列存储、可伸缩、实时读写、分布式、高性能高可靠；存储非结构化数据，基于列而非行

结构：Master/Slave架构，主节点HMaster，从节点为HRegionServer。

> HMaster是由zookeeper的选举机制选出的唯一管理节点。HMaster通过zookeeper分配协调HRegionServer崩溃时的Regions，HBaseClient也是通过zookeeper，得到HMaster、HRegionServer、-ROOT-核心数据之后，才能访问HRegionServer

![](https://uploadfiles.nowcoder.com/images/20190524/4206388_1558706443205_D3529FCA4176D9B2F36EADAC74ABA0C4)

## Region ##
1. HBase分布式存储和负载均衡的最小单位。可以是Table划分出来的Region，也可以是.META.表划分出来的Region。
一个HRegionServer管理维护多个Regions实例HRegion，但是一个Region只存在于一个RegionServer，物理上存在于HDFS。HRegionServer还负责维护HLog。记录着管理的所有Regions的操作日志
2. HLog是用来做灾难备份的，采用预写式日志WAL(Write-Ahead Log)。一个HRegionServer对应着一个HLog，因此HLog中记录着所有HRS管理的所有的Region，避免对多个文件读写减少了寻址次数提高性能。一个HRS故障之后需要HMaster对HLog进行拆分，然后对Region进行重新分配。
3. 每个Region由若干个Store组成。**一个Store对应一个列族下的所有数据**。一个Store只有一个MemStore，用来缓存数据，缓存到一定数量的时候就持久化到本地变为StoreFile，因此SF可以有多个，但MS只有一个。其中SF是以HFile的格式存储于HDFS之中。

![](https://uploadfiles.nowcoder.com/images/20190524/4206388_1558706458776_30D3AF1CE259BA1F0F2E8E421B1D3E54)

## HBase写操作 ##
1. HClient先通过Zookeeper(得到HMaster、HRegionServer、-ROOT-核心数据)，找到需要访问的HRegionServer
2. 和HRegionServer建立连接，向Region提交变更，写入WAL日志和MemStore中
3. 当MS达到阈值1之后，启动单独的线程持久化为SF，SF文件足够多高于阈值2的时候就合并(Compact)成一个SF，当单个的SF文件足够大高于阈值3的时候就对当前的Region进行拆分(Split)成两个Regions，并由HM分发到其他的HRS中实现负载均衡。
4. 在Compact的过程中会对SF进行版本合并和数据删除，即HBase会一直增加数据，只有在合并的过程中才会进行更新和删除操作。

## HMaster作用 ##
1. 将Regions分配给HMS&协调HMS之间的负载&维护集群的状态
2. 通过zookeeper感知发生故障的HMS，获取并处理其对应的HLog，将故障的Regions重新分配
3. 负责管理表的Schema和对元数据的操作，用户对Table的增删改查操作

## HRegionServer作用 ##
1. 相应用户的I/O请求，向HDFS中读写文件
2. 管理多个HRegion对象
3. HRegion中的StoreFile过大时进行Split操作生成两个新的Regions，父Region下线，新的Regions被HM分到HRegionServer中

## 元数据表 ##
1. 用户表的Regions的元数据存储于.META.表中，随着Regions变多，记录Regions的元数据的.META.表也变大，因此.META.表也需要分裂成多个Regions。
2. .META.的Regions的元数据又保存于-ROOT-表(不可再分，可以理解为只有一个Region)中，zookeeper记录-ROOT-表的位置


	//HClient最多三次就能找到Regions了
	HClient=>zookeeper=>-ROOT-=>.META.=>Regions
> 其中为了提高访问速度，.META.表的Region全都保存在内存中。

1. 客户端访问Regions之前会先查看本地的缓存。缓存包括-ROOT-、.META.表和Regions的位置信息。
2. 没有缓存就询问有Regions元数据的.META.表所在的HRegionServer
3. .META.表也没查到就找有.META.表元数据Region的-ROOT-表，从而找到.META.继而找到Regions
4. 若前面的信息全部失效就通过zookeeper重新定位-ROOT-、.META.表以及Regions的位置信息。此时需要进行6次网络来回才能定位到Regions


![](https://uploadfiles.nowcoder.com/images/20190524/4206388_1558706472244_73AC7C87A9A6D2EB3C6C3DEB988F62B4)


## zookeeper ##
1. 用来存储-ROOT-表的地址、HMaster的地址和HRegionServer的地址
2. HM通过ZK感知HRS的状态
3. HBase中可以启动多个HMaster，但是ZK的选举机制保证集群中只有一个HM为当前集群的master
4. 当HM出现单点故障，会立即选出一个新HM的作为master