# kafka

## kafka 安装
1. 下载安装包解压，有自带的zookeeper，最好使用独立的zookeeper
2. zookeeper安装解压后配置 `conf/zoo.cfg`，配置`dataDir & dataLogDir & clientPort(默认2181)`；如果是zookeeper集群需要配置`server.idNum = 192.168.213.141:2888:3888`和`${dataDir}/myid`文件，其中myid文件中保留`idNum`的值
3. 安装好zookeeper之后启动服务`bin/zkServer start` 
4. 解压Kafka压缩包，配置`config/server.properties`，主要包括(1)`zookeeper.connect=192.168.213.142:2181`，即zookeeper的地址(2)`log.dirs=${logDir}`代表Kafka的日志存储地址(3)`broker.id=idNum`，broker理解为一个Kafka服务器，这个ID用于唯一表示这个server
5. 配置好启动Kafka服务`bin/kafka-server-start.sh config/server.properties` 
6. 创建Kafka主题`bin/kafka-topics.sh --create --zookeeper 192.168.213.142:2191 --replication-factor 1 -- partitions 1 --topic test-1205`
7. 查看所有Kafka主题`bin/kafka-topics.sh -list -zookeeper 192.168.213.142:2191`，输出当前的所有topic
8. 创建生产者往主题中写数据`bin/kafka-console-producer.sh --broker-list 192.168.213.142:9092 --topic test-1205`，进入控制台模式，开始向topic `test-1205`中写数据
9. 创建消费者消费主题中的数据`bin/kafka-console-consumer.sh --bootstrap-server 192.168.213.142:9092 --topic test-1205 --from-beginning` 
10. 关闭Kafka服务`bin/kafka-server-stop.sh`，关闭zookeeper服务`bin/zkServer.sh stop` 
