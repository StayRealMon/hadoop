## ubuntu2 ##
> 2019-05-03 06:58:45,564 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu2/127.0.0.1:58808. Already tried 7 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 06:58:46,565 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu2/127.0.0.1:58808. Already tried 8 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 06:58:47,565 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu2/127.0.0.1:58808. Already tried 9 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 06:58:47,567 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : java.net.ConnectException: Call From ubuntu2/127.0.0.1 to ubuntu2:58808 failed on connection exception: java.net.ConnectException: Connection refused; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused
>         at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
>         at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
>         at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
>         at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
>         at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:792)
>         at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:732)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1480)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1413)
>         at org.apache.hadoop.ipc.WritableRpcEngine$Invoker.invoke(WritableRpcEngine.java:242)
>         at com.sun.proxy.$Proxy9.getTask(Unknown Source)
>         at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:132)
> Caused by: java.net.ConnectException: Connection refused
>         at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
>         at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:717)
>         at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:206)
>         at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
>         at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:495)
>         at org.apache.hadoop.ipc.Client$Connection.setupConnection(Client.java:615)
>         at org.apache.hadoop.ipc.Client$Connection.setupIOstreams(Client.java:713)
>         at org.apache.hadoop.ipc.Client$Connection.access$2900(Client.java:376)
>         at org.apache.hadoop.ipc.Client.getConnection(Client.java:1529)
>         at org.apache.hadoop.ipc.Client.call(Client.java:1452)
>         ... 4 more
> 
> 2019-05-03 06:58:47,568 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Stopping MapTask metrics system...
> 2019-05-03 06:58:47,568 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system stopped.
> 2019-05-03 06:58:47,569 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system shutdown complete.


## ubuntu3 ##
> 2019-05-03 07:39:07,608 INFO [main] org.apache.hadoop.metrics2.impl.MetricsConfig: loaded properties from hadoop-metrics2.properties
> 2019-05-03 07:39:07,665 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Scheduled snapshot period at 10 second(s).
> 2019-05-03 07:39:07,665 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system started
> 2019-05-03 07:39:07,672 INFO [main] org.apache.hadoop.mapred.YarnChild: Executing with tokens:
> 2019-05-03 07:39:07,673 INFO [main] org.apache.hadoop.mapred.YarnChild: Kind: mapreduce.job, Service: job_1556894213476_0001, Ident: (org.apache.hadoop.mapreduce.security.token.JobTokenIdentifier@6283d8b8)
> 2019-05-03 07:39:07,831 INFO [main] org.apache.hadoop.mapred.YarnChild: Sleeping for 0ms before retrying again. Got null now.
> 2019-05-03 07:39:08,860 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 0 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:09,861 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 1 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:10,862 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 2 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:11,863 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 3 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:12,865 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 4 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:13,866 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 5 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:14,866 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 6 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:15,869 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 7 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:16,869 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 8 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:17,870 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 9 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
> 2019-05-03 07:39:17,873 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : java.net.ConnectException: Call From ubuntu3/127.0.0.1 to ubuntu3:41563 failed on connection exception: java.net.ConnectException: Connection refused; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused
> 	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
> 	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
> 	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
> 	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
> 	at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:792)
> 	at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:732)
> 	at org.apache.hadoop.ipc.Client.call(Client.java:1480)
> 	at org.apache.hadoop.ipc.Client.call(Client.java:1413)
> 	at org.apache.hadoop.ipc.WritableRpcEngine$Invoker.invoke(WritableRpcEngine.java:242)
> 	at com.sun.proxy.$Proxy9.getTask(Unknown Source)
> 	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:132)
> Caused by: java.net.ConnectException: Connection refused
> 	at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
> 	at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:717)
> 	at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:206)
> 	at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
> 	at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:495)
> 	at org.apache.hadoop.ipc.Client$Connection.setupConnection(Client.java:615)
> 	at org.apache.hadoop.ipc.Client$Connection.setupIOstreams(Client.java:713)
> 	at org.apache.hadoop.ipc.Client$Connection.access$2900(Client.java:376)
> 	at org.apache.hadoop.ipc.Client.getConnection(Client.java:1529)
> 	at org.apache.hadoop.ipc.Client.call(Client.java:1452)
> 	... 4 more
> 
> 2019-05-03 07:39:17,875 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Stopping MapTask metrics system...
> 2019-05-03 07:39:17,875 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system stopped.
> 2019-05-03 07:39:17,876 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system shutdown complete.

## Solution ##
注释掉/etc/hosts文件中的127.0.0.1
> \#127.0.0.1      ubuntu1
192.168.213.141 ubuntu1
192.168.213.142 ubuntu2
192.168.213.143 ubuntu3



## Result ##
> 23952 Master
> 23570 NameNode
> 23812 SecondaryNameNode
> 24329 Jps
> 24075 ResourceManager
> root@ubuntu1:/usr/local/hadoop-2.7.7/sbin# yarn jar ../share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.7.jar pi 2 10
> Number of Maps  = 2
> Samples per Map = 10
> Wrote input for Map #0
> Wrote input for Map #1
> Starting Job
> 19/05/03 21:21:42 INFO client.RMProxy: Connecting to ResourceManager at master/192.168.213.141:8032
> 19/05/03 21:21:43 INFO input.FileInputFormat: Total input paths to process : 2
> 19/05/03 21:21:43 INFO mapreduce.JobSubmitter: number of splits:2
> 19/05/03 21:21:43 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1556943677275_0001
> 19/05/03 21:21:43 INFO impl.YarnClientImpl: Submitted application application_1556943677275_0001
> 19/05/03 21:21:43 INFO mapreduce.Job: The url to track the job: http://master:8088/proxy/application_1556943677275_0001/
> 19/05/03 21:21:43 INFO mapreduce.Job: Running job: job_1556943677275_0001
> 19/05/03 21:21:49 INFO mapreduce.Job: Job job_1556943677275_0001 running in uber mode : false
> 19/05/03 21:21:49 INFO mapreduce.Job:  map 0% reduce 0%
> 19/05/03 21:21:55 INFO mapreduce.Job:  map 50% reduce 0%
> 19/05/03 21:21:58 INFO mapreduce.Job:  map 100% reduce 0%
> 19/05/03 21:22:00 INFO mapreduce.Job:  map 100% reduce 100%
> 19/05/03 21:22:00 INFO mapreduce.Job: Job job_1556943677275_0001 completed successfully
> 19/05/03 21:22:00 INFO mapreduce.Job: Counters: 49
>         File System Counters
>                 FILE: Number of bytes read=50
>                 FILE: Number of bytes written=369666
>                 FILE: Number of read operations=0
>                 FILE: Number of large read operations=0
>                 FILE: Number of write operations=0
>                 HDFS: Number of bytes read=522
>                 HDFS: Number of bytes written=215
>                 HDFS: Number of read operations=11
>                 HDFS: Number of large read operations=0
>                 HDFS: Number of write operations=3
>         Job Counters
>                 Launched map tasks=2
>                 Launched reduce tasks=1
>                 Data-local map tasks=2
>                 Total time spent by all maps in occupied slots (ms)=9772
>                 Total time spent by all reduces in occupied slots (ms)=7053
>                 Total time spent by all map tasks (ms)=4886
>                 Total time spent by all reduce tasks (ms)=2351
>                 Total vcore-milliseconds taken by all map tasks=4886
>                 Total vcore-milliseconds taken by all reduce tasks=2351
>                 Total megabyte-milliseconds taken by all map tasks=7504896
>                 Total megabyte-milliseconds taken by all reduce tasks=7222272
>         Map-Reduce Framework
>                 Map input records=2
>                 Map output records=4
>                 Map output bytes=36
>                 Map output materialized bytes=56
>                 Input split bytes=286
>                 Combine input records=0
>                 Combine output records=0
>                 Reduce input groups=2
>                 Reduce shuffle bytes=56
>                 Reduce input records=4
>                 Reduce output records=0
>                 Spilled Records=8
>                 Shuffled Maps =2
>                 Failed Shuffles=0
>                 Merged Map outputs=2
>                 GC time elapsed (ms)=144
>                 CPU time spent (ms)=1620
>                 Physical memory (bytes) snapshot=716242944
>                 Virtual memory (bytes) snapshot=10115973120
>                 Total committed heap usage (bytes)=567803904
>         Shuffle Errors
>                 BAD_ID=0
>                 CONNECTION=0
>                 IO_ERROR=0
>                 WRONG_LENGTH=0
>                 WRONG_MAP=0
>                 WRONG_REDUCE=0
>         File Input Format Counters
>                 Bytes Read=236
>         File Output Format Counters
>                 Bytes Written=97
> Job Finished in 17.26 seconds
> Estimated value of Pi is 3.80000000000000000000
> root@ubuntu1:/usr/local/hadoop-2.7.7/sbin#
> root@ubuntu1:/usr/local/hadoop-2.7.7/sbin# sh ./shut-all.sh
> stop-yarn.sh
> stopping yarn daemons
> stopping resourcemanager
> tiansir2: stopping nodemanager
> tiansir3: stopping nodemanager
> no proxyserver to stop
> stop-all.sh
> tiansir3: stopping org.apache.spark.deploy.worker.Worker
> tiansir2: stopping org.apache.spark.deploy.worker.Worker
> stopping org.apache.spark.deploy.master.Master
> stop-dfs.sh
> Stopping namenodes on [master]
> master: stopping namenode
> tiansir3: stopping datanode
> tiansir2: stopping datanode
> Stopping secondary namenodes [master]
> master: stopping secondarynamenode
> shut-all.sh Succeed!
> 26682 Jps
> root@ubuntu1:/usr/local/hadoop-2.7.7/sbin#

