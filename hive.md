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