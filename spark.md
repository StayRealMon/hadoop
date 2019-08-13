## 面试 ##
|@| zookeeper做分布式锁
|@| flink了解哪些，它的基本架构原理
> flink on yarn 的任务提交和任务调度 & 两种window(count||time)三种窗口方式(tumble/slide/session)以及三个time(event/ingestion/process) & watermark

|@| 很大的m*n的数组中，每一行有序，每一列无序，如何求其topk
|@| 短url映射长url，系统qps5000，要求设计一套完整的高可用分布式系统，设计数据库结构，负载均衡等，且要求可以1s内查询到出现次数前100的Url
> 全局自增id做可逆哈希(发号器，单双号，自增id数字转62进制存储，lru淘汰机制，短url存在缓存数据库中有时效可延长，命中后返回302重定向可记录点击率)，lru缓存常用的

|@| kafka的原理，kafka作为消息队列和redis/rabbitMQ的区别；
> kafka基于disk典型的生产消费者模式，消息可回溯(offset/timestamp)；RabbitMQ基于内存P2P模式数据消费后即删除
> kafka典型的pull(push会造成consumer崩溃；pull会使consumer轮询)

|@| 一个topic中的partition是不是一定散布在同一个broker中？
> 不一定。一个topic由多个partition组成且分布在不同的broker中，有利于并发读。partition有备份机制都放在一个节点宕机就凉了

|@| 如果要保证消息全局有序，怎么做？
|@| leader选举是怎么选的？
> 维护动态ISR，有leader挂到就从set里面直接选一个，等待其他机器加入ISR；leader负责读写，follower被动replicate


|@| kafka中consumer怎么保持状态的？
|@| Exactly Once？
## 实时 ##
> 1. 实时部分：业务主要为发单量、行程量、成交单量，通过flink实时消费数据库WAL变更日志，进行实时的聚合统计，在某些场景下需要用redis缓存订单的中间计算状态,将最终计算结果输出至HBase，供实时接口查询，形成订单滚动大屏的效果
> 2. 近线业务：通过kafka+flume和自定义flume interceptor来消费WAL日志，并进行replay数据，近线还原数据库数据至数仓，目前延迟是20分钟，此延迟可以配置，不过最短延迟不要小于5min
> 3. 离线部分：业务方需要查询几天前的数据，采用标准的T+1数仓建设方式，按天抽取数据，形成离线数仓
> 4. 针对单车业务实时同步单车业务数据表并落数仓表：rb.kafka_t_bike_schedule_detail_log
> 5. 总量17e/d，单车1.5e/d，压测会翻倍

## 实时数仓 ##
> ODS层:通过kafka传输实时数据，主要分为埋点数据、数据库binlog变化日志等
> 明细层: 对ODS层进行merge和过滤等操作形成原始的明细层，存储在kafka以便下游实时消费和处理
> 汇总层：一方面为应用层提供明细数据或汇总明细数据，需要存储至Kafka,方便应用层实时消息和处理；另一方面，充当数据输出层面存储至HBase,可以支持数据查询数据
> 应用层：实时处理的最后一站，实时消息汇总层数据，按照业务需求进行聚合、实时补全维度信息，处理完成后可以按照业务需要输出至Druid\ElasticSearch\PG\HBase任意一种或多种存储介质，为应用层做实时报表、实时大盘提供支撑
> 实时维度层：通过HBase存储数据，同时需要实时消息维度变化的消息，及时更新至HBase的维度表，保证业务实时获取维度信息
> 实时维度补全&中间结果dump处理，将存储至kafka的数据以flume+kafka的近线方式dump到Hive离线数仓，方便定位每个环节的数据，保证实时结果可验证和出问题时结果可修复

## scala ##


## spark ##
tachyon:in-memory file system

Stream Processing	流处理
Ad-hoc Queries	即席查询
Batch Processing	批处理

### MR的Shuffle过程和Spark的区别 ###
split 1：1 map任务；缓冲区memory持久化到本地中时进行partition和sort，spill to disk；再把持久化的小文件merge成为一个较大的文件；
reduce任务个数1：1 key的hash值；shuffle过程把相同key的文件拉到一起再进行merge和sort，最后执行reduce任务输出结果
map结束到reduce开始之间称为shuffle

spark会将某些步骤基于内存处理，避免磁盘I/O迭代


### SparkConf &SparkContext###
SparkConf:设置spark的运行模式(Local/Standalone/yarn/mesos)；app的名称和资源(memory&core)设置
SparkContext:通往集群的唯一通道，通过sc获取第一个rdd


### RDD ###
Resilient Distributed Dataset弹性分布式数据集，逻辑概念，实际中不存数据(1 task处理1partition，partition可以分布在多个节点上，partition也不存数据)
**弹性**体现在
1. partition个数可多(多核多task进行)可少(减少启动task时间)
2. 有血缘依赖关系的容错机制
通过sc.textfile(...)获取第一个rdd1(split对应partition)，由一系列partition(block)组成，通过rdd1.flatmap变成rdd2，再通过rdd2.map变成rdd3。其中rdd123的partition个数相同，flatmap和map称为算子，算子逻辑上作用于rdd，物理上作用于组成rdd的partition，生成下一个rdd对应的partition
**特性**
1. RDD由partition组成
2. 算子作用于partition
3. RDD之间有血缘关系Lineage
4. 分区器作用在KV格式的RDD中
5. partition对外提供最佳的计算位置(计算移动数据不移动)

### DAG ###
RDD的Lineage关系有向无环可以看作DAG但并不是


### Driver/Worker ###
Driver发送task给Worker，Worker把result返回给Driver

### Transformer/Action ###
Transformation算子懒加载，遇到Action的时候才触发，Action会一直往上找到最原始的RDD，才开始运行。一个App中的action数量和运行中的job数量一致。可以考虑持久化RDD，否则每次都要从头加载RDD。

持久化算子包括
1. rdd.cache()将RDD存储在内存中，懒执行算子；
2. rdd.persist()手动指定持久化级别disk/Memory/OffHeap(堆外内存Techyon)/Deserialized/replication[内存不够了再放磁盘]；
3. checkpoint将数据存在磁盘中，切断rdd的lineage，application跑完之后persist持久化的数据被回收，而checkpoint会永久存储于disk供下一个app使用[先由action触发回溯到数据源，计算到被标记的rdd的时候，把rdd结果setCheckpoint到disk，切断lineage])

持久化算子的最小单位都是partition。

Transformation(filter/map/flatmap/reduceByKey/sample)
Action(foreach/count/collect)


## Spark SQL ##
1. Shark依赖于Hive，SparkSQL脱离了Hive限制，且SparkSQL支持查询原生的RDD，查询结果为DF，DF和RDD可以互转
2. Spark on Hive，即SparkSQL，其中Hive作为存储，解析优化和执行引擎都是Spark
3. Hive on Spark，解析和优化都是Hive，Spark作为执行引擎，底层不是MR而是Spark job
4. DF是由列式RDD组成的，由sqlContext.read(文件)或者sqlContext.sql(sql语句)。df = sqlContext.read().format().load(); df.show(); df.preintSchema(); df.registerTempTable()可以将DF注册为临时表，临时表是个指针，不是disk或者memory中的文件
5. df和RDD互相转化**df->RDD**:Java<Row> rdd = df.javaRDD() **RDD->df**:sqlContext.createDataFrame(RDD, obj.class)利用反射机制，自定义类要实现序列化接口(节点之间传送对象的时候必须序列化，)

## Kafka ##
分布式消息队列：系统之间解耦；峰值压力缓冲，给后续提供稳定输入；异步通信；高吞吐；存磁盘不丢失，顺序写顺序读，直接append到文件之后；分布式partition有副本
producer&consumer&broker(处理读写请求和存储消息，通过zookeeper协调broker节点)&topic(消息队列/分类)
1. 一个topic由多个partition组成(便于扩展，提高并发度)，每个partition内部消息强有序，每个消息都有offset，提高并行度，每个consumer只能读取一个partition；partition是严格FIFO的，topic不是严格的
2. n partition ： 1 broker，一个partition仅有唯一broker管理维护。
3. 消息直接写入文件不存储在内存中
4. producer以(轮询负载均衡或者基于hash)决定往某一个partition写消息
默认保存一周，不是消费完就删除
5. consumer有group的概念，topic中的消费仅可被一个group消费一次
6. group内是queue消费模型，不同的consumer消费不同的partition，没消费完可以被其他consumer继续消费；consumer利用zookeeper维护消费到partition的某个offset；所有consumer都在一个group就等价于queue，每个group只有一个consumer就等价于发布订阅系统
7. zk协调broker/存储元数据/consumer的offset信息/topic信息和partition信息

> kafka也是依赖于zk，需要有zk环境的支持；配置kafka的config/*.properties；启动zk/kafka(bin/*start.sh config/*.properties)
> 启动之后可以创建查看删除topic(bin/kafka-topic.sh --create/describe/delete)
> 在producer/consumer窗口启动消息控制台(bin/kafka-console-*.sh)

### 零拷贝 ###
1. 高性能的将数据从页面缓存发送到socket的系统函数(Linux中是sendfile)
> 为什么kafka比rm快，答了零拷贝，具体实现原理答错了，应该是避免复制数据到应用缓冲，直接使用sendfile传输数据
> 网卡直接从主存中读取数据，不需要disk → read memory → application memory → write memory，直接disk → memory → consumer
>> 1. 操作系统把数据从文件拷贝内核中的页缓存中
>> 2. 应用程序从页缓存从把数据拷贝自己的内存缓存中
>> 3. 应用程序将数据写入到内核中socket缓存中
>> 4. 操作系统把数据从socket缓存中拷贝到网卡接口缓存，从这里发送到网络上。
![](https://img-blog.csdn.net/20180906202007477?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RzaGZfMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 选举 ###
集群由一个节点controller负责leader的选举和所有partition的均匀分布，使每个节点都会存在一定比例的leader
1. 只有**leader 负责读写**，**follower只负责备份(被动)**，如果leader宕机的话,Kafaka动态维护了一个同步状态的副本的集合（a set of in-sync replicas），简称ISR(针对每个Topic维护一个ISR),ISR中有f+1个节点，就可以允许在f个节点down掉的情况下不会丢失消息并正常提供服。ISR的成员是动态的，如果一个节点被淘汰了，当它重新达到“同步中”的状态时，他可以重新加入ISR。因此如果leader宕了，**直接从ISR中选择一个follower**就行；不同的topic下不同的partitioner有不同的leader，避免n×n的复杂链路，保证了一致性；ISR(0,1,all)反馈ack之后leader反馈commit给client
![](https://images2018.cnblogs.com/blog/137084/201806/137084-20180616151857110-745671907.png)

2. 区别于ZK：zookeeper使用了ZAB(Zookeeper Atomic Broadcast)协议，保证了leader,follower的一致性，**leader 负责数据的读写**，而**follower只负责数据的读**，如果follower遇到**写操作，会提交到leader**;超过半数当leader；leader 的更新操作是按照queue队列发给follower的，且leader收到超过半数的ack就会给client返回commit消息，但是有可能更新还未成功写入到follower中，且有时差
![](https://images2018.cnblogs.com/blog/137084/201806/137084-20180616151745378-1678869628.png)

### producer写入流程 ###
1. 先从broker-list获取partition的leader
2. producer和leader连接交互传数据(ack设置为0,1,all)
3. leader写消息到log
4. follower从leader中pull消息并写入自身log
5. 最后leader给producer反馈ack

> 解耦：消息系统在处理过程中插入一个隐含、基于数据的接口层。相当于一个MQ，producer会比consumer处理速度快，**解耦异步缓冲**
> 冗余：消息队列持久化，防止数据丢失。
> 扩展性：消息队列解耦处理过程，容易扩展处理过程。
> 可恢复性：处理过程失效，恢复后可继续处理。
> 顺序保证：消息队列保证顺序。Kafka保证一个Partition内消息有序。
> 异步通信：消息队列允许消息加入队列，等需要时再处理。

### Message Set 数据压缩###
> 支持GZIP和Snappy压缩协议；端到端的压缩
> 客户端的消息可以一起被压缩后送到服务端，并**以压缩后的格式写入**日志文件，**以压缩的格式发送**到consumer，消息从producer发出到consumer拿到都被是压缩的，只有在consumer**使用的时候才被解压缩**，所以叫做“端到端的压缩”。

## flink ##
flink1.6+hadoop2.7+scala2.12
/conf/.yaml&slave
### 任务提交 ###
**YARN**：flink client找RM提交申请启动JobM，JM从HDFS加载jar包等资源，向AM申请资源，RM根据所需返回资源，JM通知申请到的NM节点启动taskManager

### 任务调度 ###
flink client先把code转换成DataFlow Graph，发送给JM之后，JM根据Graph的关系划分为task并分到TM上，并启动slot进行parallelize计算

### datasource ###
StreamExecutionEnvironment.addSource(sourceFunction)
1. sourceFunction包括并行和非并行；自带实现好的有fromCollection()fromElements()fromParallelCollection()generateSequence
2. DataStream<> ds = env.readTextFile(path)//socketTextStream(port)
3. 自定义SF需要实现SourceFunction 接口，有两个方法run()和cancel()

### datasink ###
1. 接口类SinkFunction有一个invoke()方法和RichSinkFunction()抽象类
2. 自定义SF继承RichSinkFunction()，重写invoke()方法，写入Kafka/Mysql等中

### Transformation ###
处理datasource，有map/FlatMap/Filter/KeyBy(返回为KeyedStream格式)/Reduce/Fold/Aggregations/Window/WindowAll/Union/WindowJoin/Split/Select/Project

### datastream API ###
三步操作：source/transformation/sink
基本操作：1基于单条记录filtermap2基于窗口window3合并和拆分流union/join/connect/split
基本转换：
![](https://uploadfiles.nowcoder.com/images/20190730/4206388_1564494354701_572736687DEDA6D4B1B0B8477DE6C952)

window理解为纵向切分。keyby理解为横向切分，将相同key的分发到一起，类似于map？
物理分组：dataStream.global/boardcast/forward/shuffle/rebalance

###time & window###
1. event time(事件的创建时间)&Ingestion time(数据进入flinnk事件)&windows process time(基于时间操作算子的本地系统时间，默认时间)
2. 对time进行聚合，从而划分窗口，在windows内部操作算子；windows分为count window(不是数据量够count就执行，是相同的key达到count时才会执行)和time window两大类(默认按照process time处理)
3. tumbling(不重叠，windowsize)/sliding(重叠，windowsize&windowslide)/session(session是time window特有的，两个session的process time 大于windowsize时候，pro time前面的就被一个session window处理)
4. window是左闭右开的

### Event Time & Window ###
flink 时间轴默认使用processTime，生产环境一般使用EventTime
1. 创建Env后，声明使用eventTime
2. window会先被创建，然后等待数据等待触发，

**延时触发机制watermark**：用来处理乱序时间，当window end time小于watermark时会触发这个window；数据流中的waterMark用于表示所有数据携带的一个隐藏信息
(用来标记数据时间，类似一个阈值？不再接收到比wm小的时间数据，其余的再来晚的数据就被抛弃)
### flink sql ###
高层声明式api/自动优化/流批一体
**聚合**：window-aggregate&group-aggregate
window-aggregate(窗口内的小型批处理)：tumble(固定)/hop(滑动)/session(会话)
group-aggregate(没有窗口，来一条处理一条，结果是在不断更新，不适合kafka适合mysql等可更新数据库)：
> win-aggr：按时，一条只处理一次，appendStream不更新，及时处理历史数据，后可接任意sink
> 
> group-aggr：提前输出，一条输出N个结果(sink压力)，updateStream更新，状态无限增长(根据精确性设置TTL)，后接可更新结果表Hbase/mysql

建表不支持DDL，用配置文件生成

CEP规则匹配?

https://www.jianshu.com/p/0a15d44405cc