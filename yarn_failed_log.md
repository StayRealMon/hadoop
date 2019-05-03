## ubuntu2 ##
2019-05-03 06:58:45,564 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu2/127.0.0.1:58808. Already tried 7 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 06:58:46,565 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu2/127.0.0.1:58808. Already tried 8 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 06:58:47,565 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu2/127.0.0.1:58808. Already tried 9 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 06:58:47,567 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : java.net.ConnectException: Call From ubuntu2/127.0.0.1 to ubuntu2:58808 failed on connection exception: java.net.ConnectException: Connection refused; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
        at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:792)
        at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:732)
        at org.apache.hadoop.ipc.Client.call(Client.java:1480)
        at org.apache.hadoop.ipc.Client.call(Client.java:1413)
        at org.apache.hadoop.ipc.WritableRpcEngine$Invoker.invoke(WritableRpcEngine.java:242)
        at com.sun.proxy.$Proxy9.getTask(Unknown Source)
        at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:132)
Caused by: java.net.ConnectException: Connection refused
        at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
        at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:717)
        at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:206)
        at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
        at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:495)
        at org.apache.hadoop.ipc.Client$Connection.setupConnection(Client.java:615)
        at org.apache.hadoop.ipc.Client$Connection.setupIOstreams(Client.java:713)
        at org.apache.hadoop.ipc.Client$Connection.access$2900(Client.java:376)
        at org.apache.hadoop.ipc.Client.getConnection(Client.java:1529)
        at org.apache.hadoop.ipc.Client.call(Client.java:1452)
        ... 4 more

2019-05-03 06:58:47,568 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Stopping MapTask metrics system...
2019-05-03 06:58:47,568 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system stopped.
2019-05-03 06:58:47,569 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system shutdown complete.


## ubuntu3 ##
2019-05-03 07:39:07,608 INFO [main] org.apache.hadoop.metrics2.impl.MetricsConfig: loaded properties from hadoop-metrics2.properties
2019-05-03 07:39:07,665 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Scheduled snapshot period at 10 second(s).
2019-05-03 07:39:07,665 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system started
2019-05-03 07:39:07,672 INFO [main] org.apache.hadoop.mapred.YarnChild: Executing with tokens:
2019-05-03 07:39:07,673 INFO [main] org.apache.hadoop.mapred.YarnChild: Kind: mapreduce.job, Service: job_1556894213476_0001, Ident: (org.apache.hadoop.mapreduce.security.token.JobTokenIdentifier@6283d8b8)
2019-05-03 07:39:07,831 INFO [main] org.apache.hadoop.mapred.YarnChild: Sleeping for 0ms before retrying again. Got null now.
2019-05-03 07:39:08,860 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 0 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:09,861 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 1 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:10,862 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 2 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:11,863 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 3 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:12,865 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 4 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:13,866 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 5 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:14,866 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 6 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:15,869 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 7 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:16,869 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 8 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:17,870 INFO [main] org.apache.hadoop.ipc.Client: Retrying connect to server: ubuntu3/127.0.0.1:41563. Already tried 9 time(s); retry policy is RetryUpToMaximumCountWithFixedSleep(maxRetries=10, sleepTime=1000 MILLISECONDS)
2019-05-03 07:39:17,873 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : java.net.ConnectException: Call From ubuntu3/127.0.0.1 to ubuntu3:41563 failed on connection exception: java.net.ConnectException: Connection refused; For more details see:  http://wiki.apache.org/hadoop/ConnectionRefused
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:792)
	at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:732)
	at org.apache.hadoop.ipc.Client.call(Client.java:1480)
	at org.apache.hadoop.ipc.Client.call(Client.java:1413)
	at org.apache.hadoop.ipc.WritableRpcEngine$Invoker.invoke(WritableRpcEngine.java:242)
	at com.sun.proxy.$Proxy9.getTask(Unknown Source)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:132)
Caused by: java.net.ConnectException: Connection refused
	at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
	at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:717)
	at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:206)
	at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
	at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:495)
	at org.apache.hadoop.ipc.Client$Connection.setupConnection(Client.java:615)
	at org.apache.hadoop.ipc.Client$Connection.setupIOstreams(Client.java:713)
	at org.apache.hadoop.ipc.Client$Connection.access$2900(Client.java:376)
	at org.apache.hadoop.ipc.Client.getConnection(Client.java:1529)
	at org.apache.hadoop.ipc.Client.call(Client.java:1452)
	... 4 more

2019-05-03 07:39:17,875 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: Stopping MapTask metrics system...
2019-05-03 07:39:17,875 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system stopped.
2019-05-03 07:39:17,876 INFO [main] org.apache.hadoop.metrics2.impl.MetricsSystemImpl: MapTask metrics system shutdown complete.