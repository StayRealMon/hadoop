### 安装模式 ###
内嵌模式(Derby/一个活动用户)&本地模式(MetaStore位于Hive进程中)&完全远程模式(MetaStore位于数据库中，支持多用户连接)
### 创建表&分区 ###

	create [EXTERNAL] table tablename(
	col1 int,
	col2 timestamp,
	col3 string,
	col4 array<int>,
	col5 map<int,string>)
	//分区字段不能与前面定义的列名相同，加载的时候会给分区赋值(注意分区粒度大小)用于过滤导入的数据
	partitioned by (col6, int)
	row format delimited
	fields terminated by ','
	collection items terminated by '-'
	map keys terminated by ':'
	lines terminated by '\n'
	null defined as '?'
	[location 'hdfs_path'];


	//建立分区
	USE power_bike;
	DROP TABLE IF EXISTS t_ev_ride_appraise;
	CREATE EXTERNAL TABLE t_ev_ride_appraise
	(
	 guid      string      comment '唯一标识',
	 user_id      bigint      comment '用户GUID',
	 mobile_phone      string      comment '用户手机号',
	 order_id      string      comment '订单唯一编号',
	 ride_time      bigint      comment '骑行时长',
	 ride_distance      bigint      comment '骑行距离',
	 bike_no      string      comment '本次骑行车辆编号',
	 city_name      string      comment '城市名称',
	 appraise_type      bigint      comment '评价类型（1.好评，2.差评)',
	 tag_info      string      comment '评价标签类型 json array结构',
	 appraise_content      string      comment '评价内容',
	 create_time      string      comment '记录创建时间',
	 update_time      string      comment '记录更新时间'
	)COMMENT '骑行评价'
	PARTITIONED BY(pt string comment 'increment_partition')
	ROW FORMAT DELIMITED FIELDS TERMINATED BY '\001'
	COLLECTION ITEMS TERMINATED BY '\002'
	LINES TERMINATED BY '\n'
	STORED AS TEXTFILE
	LOCATION '/user/data/hello_0702';	
	LOAD DATA INPATH '/tmp/fake_data.txt' INTO TABLE t_ev_ride_appraise PARTITION(pt='20190702');
> Location:               hdfs://master:9000/user/data/hello_0702
> Table Type:             EXTERNAL_TABLE


### 内外部表 ###
外部表create的时候最后加上指定路径，删除的时候只删除数据库的结构，不删除元数据

内部表会将表结构和元数据全部删除
内外部选择根据实际业务

### 静态分区&动态分区 ###

	alter table table_name add partition(col6 = 10, col7 = 'BOY')
添加分区的时候必须建立在现有的分区之上
删除分区的时候会把所有存在的分区全删除
分区相当于目录

	alter table table_name drop partition(col7 = 'BOY')
删除之后col6目录之中还会有其他的col7 = 'GIRL'
### 数据加载 ###
本地加载数据相当于直接上传数据到hdfs

	load data local inpath 'file:///home/tiansir1/ad_static_feature' into table tablename' partition(col6 = 10)

也可以直接上传文件到/user/hive/ad_static_feature目录，然后用hive查(读检查)
查询插入到表中，先创建表，从一个表查，再插入到另一个表

	from table_name1 
	//查询结果插入到表
	insert overwrite table table_name2
	select col1,col2,col3
	//查询结果保存到本地文件
	insert overwrite local '/home/ts/'
	select col1,col2
	//查询结果保存到HDFS
	insert overwrite  '/root/data/'
	select col1,col2
相当于MR任务，作用：1.复制表2.中间临时表3.计算结果直接存入数据表

### Streaming ###
流式处理

	from table1
	insert overwrite table table2
	select TRANSFORM(col1,col2)
	AS (col1_1,col2_1)
	//使用脚本命令处理，将输出结果insert到新的表
	USING '/bin/cat'
	where col3>10;
EXAMPLE：
1)test.py脚本

	for line in sys.stdin:
		line = lin.strip()
		a,b,c,unixtime = line.split('\t')
		//数据格式转化
		weekday = datetime.datetime.formtimestamp(float(unixtime)).isoweekday()
		//转换后格式输出，作为流式输入
		print ('\t'.join([a,b,c,str(weekday)]))
2)hive命令，建表

	hive>create table table1(
	hive>col1 int,col2 int, col3 int, col4 int)
	hive>row format 
	hive>delimited fields terminated by '\t';
3)hive命令，转换&插入数据

	hive>add FILE test.py;
	hive>insert overwrite table table1
	hive>select TRANSFORM(col1,col2,col3,col4_pre)
	hive>USING 'test.py'
	hive>AS (col1,col2,col3,col4_pre);
	hive>from table0

TRANSFORM()中的数据是原来表格的字段fields
AS()中的数据是处理后的数据，对应insert新表的fields

## Hive API ##
### Hive UDF ###
用户定义函数(User-Defined Function)
1. 普通的UDF 一个输入产生一个输出
2. UDAF(User-Defined Aggregate Funtion) 多个输入一个输出
3. UDTF(User-Defined Table-Generating Funtion) 一个输入多个输出

> Hive支持Java编写的UDF，其他文件通过add file 和 select transform转化为流与Hive交互
> 
> Java编写普通的UDF，需要
> 
> (1)用hadoop.io.*包，继承hadoop.hive.ql.exec.UDF，并且实现evaluate方法(可以实现多个，但是方法名不变，参数可以不同)
> 
> (2)打成jar包，上传到本地路径即可
> 
> (3)hive CLI窗口ADD JAR 'path/xx.jar';create temporary function FUN as 'jar包方法名';
> 
> (4)select FUN(x,y) from table;
> 
> Java编写UDAF，需要
> 
> (1)用hadoop.io.*包，继承hadoop.hive.ql.exec.UDAF，并且实现UDAFEvaluator接口
> 
> (2)UDAFEvaluator下有5个方法：init()用于对中间结果进行初始化；iterate()接收传入的参数，进行迭代计算，返回值为boolean，需要计算的数据入口，类型为IntWritable或者TextWritable等可以序列化的类型；terminatePartial()没有参数，返回iterate中迭代后的数据；merge()接收terminatePartial的结果并合并中间值，返回值为boolean；teminate()返回最终的结果

## order by & sort by & distribute by ##
### order by ###
> order by 会对数据进行全局排序,和oracle和mysql等数据库中的order by 效果一样，
> 它只在一个reduce中进行所以数据量特别大的时候效率非常低。
> 而且当设置 ：set hive.mapred.mode=strict的时候不指定limit，执行select会报错，如下：
> LIMIT must also be specified.


### sort by ###
> sort by 是单独在各自的reduce中进行排序，所以并不能保证全局有序，一般和distribute by 一起执行，而且distribute by 要写在sort by前面
> 如果mapred.reduce.tasks=1和order by效果一样，如果大于1会分成几个文件输出每个文件会按照指定的字段排序，而不保证全局有序。
> sort by 不受 hive.mapred.mode 是否为strict ,nostrict 的影响


### distribute by ###
> 用distribute by 会对指定的字段按照hashCode值对reduce的个数取模，然后将任务分配到对应的reduce中去执行
> 就是在mapreduce程序中的patition分区过程，默认根据指定key.hashCode()&Integer.MAX_VALUE%numReduce 确定处理该任务的reduce


## Question ##
### 0628 ###
数据抽取的时候要把pg表中的数据格式转化为hive中的格式，先保存至stg层，然后再按照密级进行加密处理后保存至ods层
1. 问题1：stg层的数据表结构出现错误，修改表结构后原先分区中的表结构如何修改？(cascade/修改hive存在mysql中的表元数据)修改过后历史分区中的数据格式是否会自动转变？[解决方案1](https://blog.csdn.net/mbshqqb/article/details/70408186)
[解决方案2](https://bupt04406.iteye.com/blog/1560796)
 
2. 问题2：stg层的数据如何进行处理通过保存到ods层？即跨数据库建表+字段脱敏

### 0701 ###
1. ods层中的增量数据表比pg层原始数据表要晚，有时候会将历史分区全部读取到第一个分区，有时候只读前一个月数据，丢失了历史数据。如何判定？
2. pg源表和ods表差异：缺表/缺字段/类型不一致/comment不完整，整理出excel，想想怎么改