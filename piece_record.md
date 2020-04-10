# 待学习的零碎record


## 0408
### row_number()over()

    - 窗口函数，用于计算/取值/排序/序列。group by一般用于聚合计算函数，开窗可以在组内进行排序和取值
    - 非全局排序可以使用sort by 和 distribute by
    - distinct 能够去除完全相同的；group by能够去除之后字段相同的，且不能有多余的字段；row_number会加一列序号，排序可以以任一字段或多个字段，查询字段可以不参与分组和排序
    - row_number的执行在where/groupby之后
![功能描述](https://img-blog.csdnimg.cn/20190613222609630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY2ODI5OQ==,size_16,color_FFFFFF,t_70)


##0219
### azkaban 工作流调度器
1. crontab是linux自带的调度，适用于简单任务的调度；
2. 复杂的任务有大量的 **任务单元(脚本/程序)**以及它们之间的前后 **依赖关系**，需要完善的调度系统支持
3. 在hadoop领域，常见的工作流调度器有Oozie, Azkaban,Cascading,Hamake等
4. Oozie的配置较为复杂，azkaban定义了一种KV文件格式来建立任务之间的依赖关系，并提供一个易于使用的web用户界面维护和跟踪你的工作流
5. Azkaban将KV文件保存到mysql；将任务命令写到*.job文件中，将资源打包成zip上传到Azkaban的web界面即创建了任务。

### binlog同步
1. 主节点必须启用 **二进制日志**，记录任何修改了数据库数据的事件。
2. 从节点开启一个线程（I/O Thread)把自己扮演成mysql的客户端，通过 mysql 协议，请求主节点的二进制日志文件中的事件，有位置参数
3. 主节点启动一个线程（dump Thread），检查自己二进制日志中的事件，跟对方请求的位置对比，如果不带请求位置参数，则主节点就会从第一个日志文件中的第一个事件一个一个发送给从节点。
4. 从节点接收到主节点发送过来的数据把它放置到中继日志（Relay log）文件中，**并记录位置**（该次请求到主节点的具体哪一个二进制日志文件内部的哪一个位置）
5. 从节点启动另外一个线程（sql Thread ），把 Relay log 中的事件读取出来，并在本地再执行一次

### MYSQL中的时间
1. date年月日 time时分秒 datetime年月日时分秒 timestamp时间戳
2. unix_timestamp('y-m-d h:m:s')获得ts，from_timestamp(ts,'y-m-d h:m:s')获得datetime


##0224
###toString方法

###compareTo方法
