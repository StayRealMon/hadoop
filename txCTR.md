tiansir1@ubuntu1:~$ wc -l user_data
1396718 user_data
tiansir1@ubuntu1:~$ wc -l totalExposureLog.out
102386695 totalExposureLog.out

## ad_static_feature ##
72w条记录，7个属性

RangeIndex: 735911 entries, 0 to 735910
Data columns (total 7 columns):
ad_id            735911 non-null int64
timestamp        735911 non-null int64
account_id       735911 non-null int64
product_id       735911 non-null object
product_type     735911 non-null int64
profess_id       735911 non-null object
material_size    509252 non-null object
dtypes: int64(4), object(3)
memory usage: 39.3+ MB



ad_id | timestamp | account_id | product_id | product_type | profess_id | size 
-|-|-|-|-|-|-
|1-736053 |2014-06-03 22:31:20-2019-03-25 21:49:28 | 1-29743| 三条多值 | 1-18 | 有多值 | 有2w空值/有多值 |

读文件，转成csv格式
    #out转csv文件
	import numpy as np
	import pandas as pd
	out_data = list()
	file = open("G:\\tiansir\\dataset\\txCTR\\testA\\ad_static_feature.out",'r')
	for line in file:
	    tmp_line = line.replace(',','_')
	    tmp_line = tmp_line.replace('\t\n','\n')
	    out_data.append(tmp_line.replace('\t',','))
	#    out_data.append(line)
	print(out_data[:3])
	file.close()
	print('SUCCEED')

	file = open("G:\\tiansir\\dataset\\txCTR\\testA\\ad_static_feature.csv",'w')
	for row in out_data:
	    file.write(row)
	file.close()
	print('SUCCEED')

##读取csv
	ad_static_csv = pd.read_csv('G:\\tiansir\\dataset\\txCTR\\testA\\0ad_static_feature.csv')

##type分布
	ad_static_csv['product_type'].value_counts()

	18    244172
	1     136268
	3     109990
	8     100798
	5      71481
	13     58544
	2      13053
	15      1276
	14       173
	12       116
	7         18
	10        12
	16         4
	17         2
	6          2
	11         1
	4          1

##timestamp 分布
	list(ad_static_csv['timestamp']).count(0)
	9290


##建表
	create table ad_static_feature(
	ad_id int,
	create_time timestamp,
	account_id int,
	product_id array<int>,
	product_type int,
	profess_id array<int>,
	material_size array<int>)
	clustered by (ad_id,create_time) sorted by (ad_id,create_time) into 1 buckets
	row format delimited 
	fields terminated by ','
	collection items terminated by '_'
	map keys terminated by ':'
	lines terminated by '\n';

	desc formatted table

	load data local inpath 'file:///home/tiansir1
	ad_static_feature.csv' into table ad_static_feature1;
	Loading data to table default.ad_static_feature1
	OK
	Time taken: 2.106 seconds