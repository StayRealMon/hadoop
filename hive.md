### 面试题 ###
|@| 写过UDF，谈谈对UDF的理解，写UDF的目的，代码怎么写的
> 1. UDF函数可以直接应用于select语句，对查询结构做格式化处理后，再输出内容
> 2. 自定义UDF需要继承import org.apache.hadoop.hive.ql.exec.UDF；需要定义并实现evaluate函数
> 3. 

改造hive表后怎么进行数据一致性校验的，有没有自动化流程
数据建模，星型模型和雪花模型
hbase中row key该怎么设计
|@| 大表Join小表优化，怎么解决hive数据倾斜问题
> 分为common join 和 map join；common join就是普通的mr任务，输出文件为reduce个数，map join没有reduce阶段，小表在左先读到hashtable中，left join大表，map大表读数据遍历hashtable做连接，输出文件个数为map的个数

每天浏览页面的新用户
如何解决数据倾斜
parquet(二进制方式存储的，所以是不可以直接读取的，文件中包括该文件的数据和元数据) orc textfile

> 设计数据模型的同时思考三个问题： 业务量多大？ 并发度多少？数据存储的有效期？PostgreSQL单库QPS建议不超过5000；Redis单节点QPS建议不超过50000

|@| Hive SQL基础函数


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

## Hive 分桶 ##
1. 目的是为了数据抽样(Sampling)和map-join，在表的分区下面进行分桶操作，将原来的大表根据某个字段散列到buckets中，每个bucket会有相同哈希值的字段值，便于抽样或者根据字段进行join操作
2. buckets的个数一般和reduce的个数一致**(待确认，reduce的个数如何确定，是人为设置的吗？)**。分桶之前要先把数据存在原来的表中，然后根据字段建bucket_table，from原来的table中查数据insert into到bucket_table中，这个insert过程是MR过程，将数据从block中找到再放到新的block中，每个bucket都有自己的目录
3. 进行sampling的时候有x和y两个值需要注意，从第x个bucket开始抽y个数据，y是buckets的数量的倍数或者因子，因子的时候取多个buckets，倍数的时候取第x个bucket中的1/n数据


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
> (1)用hadoop.io.*包，继承hadoop.hive.ql.exec.UDF，并且实现evaluate方法(可以实现多个，但是方法名不变，参数可以不同)select的时候传的参数需要和UDF中实现的evaluate方法参数一致
> 
> (2)打成jar包，上传到本地路径即可
> 
> (3)hive CLI窗口ADD JAR 'path/xx.jar';create temporary function FUN as 'jar包方法名';
> 
> (4)select FUN(x,y) from table;


	import org.apache.hadoop.hive.ql.exec.UDF;
	import org.apache.hadoop.io.Text;
	
	public class CaseChange extends UDF {
	    public Text evaluate(Text input){
	        return new Text(input.toString().toLowerCase());
	    }
	    public Text evaluate(Text input, String type){
	        if (type.equals("LOWWER"))
	            return new Text(input.toString().toLowerCase());
	        else if (type.equals("UPPER"))
	            return new Text(input.toString().toUpperCase());
	        else
	            return null;
	    }
	}


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

###Sqoop & DataX ###
> 1. sqoop1没有server  且不和sqooo2兼容；
> 2. 原理是将导入作业转化为只有Map任务的MR，每个map读取一片数据，并发执行
> 3. DataX会将同步作业当成一个job，一个job是一个进程
> 4. job模块负责所有job的任务切分和task group的管理
> 5. 切分job为task便于并发执行，task为最小工作单元
> 6. job模块调用Schedule模块，Schedule将切分后的task重新组合成task group
> 7. 每一个Task都由TaskGroup负责启动，Task启动后，会固定启动Reader→Channel→Writer的线程来完成任务

## Question ##
### 0628 ###
数据抽取的时候要把pg表中的数据格式转化为hive中的格式，先保存至stg层，然后再按照密级进行加密处理后保存至ods层
1. 问题1：stg层的数据表结构出现错误，修改表结构后原先分区中的表结构如何修改？(cascade/修改hive存在mysql中的表元数据)修改过后历史分区中的数据格式是否会自动转变？[解决方案1](https://blog.csdn.net/mbshqqb/article/details/70408186)
[解决方案2](https://bupt04406.iteye.com/blog/1560796)

直接修改得时候会报错
	
	FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. Unable to alter table. The following columns have types incompatible with the existing columns in their respective positions :

可以在CLI中将参数修改，这样可以强制修改字段类型忽略可能产生的问题

	set hive.metastore.disallow.incompatible.col.type.changes=false;
读检查的时候显示不出来的数据会显示null

 
2. 问题2：stg层的数据如何进行处理通过保存到ods层？即跨数据库建表+字段脱敏

### 0701 ###
1. ods层中的增量数据表比pg层原始数据表要晚，有时候会将历史分区全部读取到第一个分区，有时候只读前一个月数据，丢失了历史数据。如何判定？(查询的时候一定先show partitions table_name，再在partition中操作查找)
2. pg源表和ods表差异：缺表/缺字段/类型不一致/comment不完整，整理出excel，想想怎么改

### 0705 idata接口开发总结 ###
1. 需求：产品要求查询接口，需要获取pg所有库的信息，和每个pg库下所有的表名字和中文注释
2. 现有的ods.file_pg_meta数据不完整(有其他用途，冗余较大)，因此选择再重新创建一张表ods.file_pg_table_meta，专门用于这个接口查询
3. 开发流程：数据源来自于pg业务库，需要抽取所需信息到hive中，再抽取到pg接口库，用于idata接口开发
4. 葛大爷先在hive ods层中建好table_meta表，我在ide环境中(数仓权限)复制葛大爷的历史任务(和pg%meta表有关)，将39个pg库名和其下的表名从pg业务库中的系统表抽取到出来到table_meta中，同时要复制start和end任务，建立数据抽取前后置任务的血缘关系，每天09:06 - 09:15执行此项任务树，保证数据更新一致


	SELECT pu.usename as user_name, pc.relname AS table_code, coalesce(obj_description(relfilenode,'pg_class'), ' ') AS table_name from pg_user pu  join pg_class pc on pu.usesysid = pc.relowner where pc.relkind = 'r' and pc.relchecks = 0 and pu.usename not in ('postgres') and \\$CONDITIONS

5. data cloud环境下确认pg的库都已经成功导入到table_meta表中，就把上面的任务树部署上线；接着在葛大爷的数据开发权限下添加新的任务，目的是将table_meta表中的数据再同步到线上dev3环境pg接口库，葛大爷建好表，psql连接，查询表结构，然后from ods层中的table_meta select所需字段到bike_report库下的table_meta中


	select concat(user_name,'_',table_name) as table_id, db as db_name,user_name,table_name,table_comment from ods.file_pg_table_meta where db = user_name

6. 最后一步就是从bike_report库下的table_meta表中提取数据做成idata接口提供给产品交付就好了。选数据源定参数，查表查字段定维度，生成sql语句测试成功最后上线交付ok√

## 0708 ##
葛大爷给了三个文档，目的是要做UDF(UDF需要一进一出，UDAF支持多进一出)，把js代码以java实现，作用是把一个输入的GeoArea对象进行扩充或者缩减，得到一块新的GeoArea，需要继承UDF并且实现evaluate函数

## 0716 ##
加入工单值班，做数据抽取
1. **加字段**先在cloud查现有字段，和pg_meta表现有字段，对比哪些是新增的。接着在cloud修改表结构cascade，执行成功后使用ide调度或者wiki查历史任务是全量或者增量，备份原任务代码，新增字段，重跑任务无误后完成√
2. **新建表**申请pg库对应的表权限，查建表时间、更新时间和数据量，判断全量同步OR增量同步，判断分区？全量同步直接create_day<${day+1}，增量好像需要${day}<create_day<${day+1}？在cloud中建表的时候，注意查询变量show create table ${table_name} 获得外部表保存的集群路径等参数(写好之后葛大爷check一下)；ide中建立抽取任务，写脚本的时候注意json::text，geo要分割成lat和lng；运行无误后cloud查询再上线即可

> 数据同步--先定分区再定同步
> 
> 1. 全量分区&全量同步    数据量小于百万级别，有更新
> 2. 全量分区&增量同步    数据量大于百万级别，有更新
>   |- 增量分区同步首次同步需要一个初始化，先把历史数据同步到 ods.table_name
>   |- 再建一个 ods.table_name_pre，用于存放前一天的全量表(未更新)
>   |- 这张表在接下来的每一天都需要同步新增的和更新的数据
>   |- 通过接下来的hive计算把 ods.table_name_pre 表中的数据覆盖写到 ods.table_name 中，注意依赖
> 
> 3. 增量分区&增量同步    增量分区类似流水表，不更新
> 
> 全量分区数据量大就增量同步，数据量小就全量同步
> 增量分区数据量需要同步新增的数据，一般不是原数据更新而是新增一条数据

## 0719 ##
单独开一条，因为两天导错了两次数据。
0718竟然是因为字段名复制粘贴错了???(加班到21:20)。
0719自以为建表语句没问题，建了三张错的表哈哈哈哈，结果两天一共1.2kw条数据目前生死未卜。建表的**地理位置要分成经纬度存**三遍啊记住了记住了记住了。(葛大爷真的牛啤好吧pg库溜到飞起，不要再因为建表语句的问题给葛大爷惹麻烦啦)

## 0726 ##
1. 大表(一般是流水日志表量大不更新)抽取：pg库存在主从备份，且有些表的备份频率会比较高，每次备份的时候会锁死行记录(保证备份过程中数据不会改变，备份完之后就像WAL一样再把操作写进来就ok了)，此时sqoop工具不能访问pg库。
2. 解决办法就是在备份的空隙用sqoop抽取较短的分区数据，一个月一周甚至五天三天，将大表的历史数据抽取到一张临时表里。再对临时表进行读取操作通过hive的**动态分区**写到新的表里，新表根据create_date创建自动分区，解决了大表历史数据同步问题。接下来就是每天增量更新新数据就可以了。
