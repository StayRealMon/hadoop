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
1. 一个topic由多个partition组成，每个partition内部消息强有序，每个消息都有offset，提高并行度，每个consumer只能读取一个partition；partition是严格FIFO的，topic不是严格的
2. n partition ： 1 broker，一个partition仅有唯一broker管理维护。
3. 消息直接写入文件不存储在内存中
4. producer以(轮询负载均衡或者基于hash)决定往某一个partition写消息
默认保存一周，不是消费完就删除
5. consumer有group的概念，topic中的消费仅可被一个group消费一次
6. group内是queue消费模型，不同的consumer消费不同的partition，没消费完可以被其他consumer继续消费；consumer利用zookeeper维护消费到partition的某个offset；
7. zk协调broker/存储元数据/consumer的offset信息/topic信息和partition信息

> kafka也是依赖于zk，需要有zk环境的支持；配置kafka的config/*.properties；启动zk/kafka(bin/*start.sh config/*.properties)
> 启动之后可以创建查看删除topic(bin/kafka-topic.sh --create/describe/delete)
> 在producer/consumer窗口启动消息控制台(bin/kafka-console-*.sh)