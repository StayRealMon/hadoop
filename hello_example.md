## 脚本样例 ##

	#!/bin/bash             ##0 注释区
	## Date : 2018-06-05
	## Author : zhuchuan
	## Desc : 换电池表
	## Source : ods.t_city,ods.t_battery_change
	
	## Target  : dw.dw_bike_chag_battery
	
	source /home/deploy/codes/dataware/config/hive_config.sh
	## 1 变量设定区
	table_name="dw_bike_chg_battery"
	
	## 2 hive 脚本区
	sql_1="
	
	0.5.除特殊情况外，不需要写hive的set参数
	
	-- 1.创建换电池临时表 #每段代码前的注释放在前面
	#1.临时表使用前先删除
	drop table if exists tmp.tmp_${table_name}_${date};
	#2.创建临时表
	create table tmp.tmp_${table_name}_${date}
	#3.换行
	as
	#4.一个字段一行,字段名前必须要有别名 别名.字段名
	select  a.user_guid
	          #5.逗号在上面字段左对齐的
	          ,count(1) as cnt
	          #6 when，else对齐
	          ,count(case when hour(unlock_date)>=6 and hour(unlock_date) <18 and capacity_before_num<70 then 1
	                             when hour(unlock_date)>=0 and hour(unlock_date) <6 and capacity_before_num<80 then 1
	                             when hour(unlock_date)>=18 and hour(unlock_date) <24 and capacity_before_num<80 then 1
	                   else null 
	                end) as cnt_valid 
	         ,case when hour(unlock_date)>=6 and hour(unlock_date)<18 then '白' 
	                   when hour(unlock_date)>=0 and hour(unlock_date)<6 then '晚' 
	                  when hour(unlock_date)>=18 and hour(unlock_date)<24 then '晚'
	                 else '' 
	            end as day_night 
	from ods.t_battery_change
	#7 一个where 条件一行 
	where a.pt='${date}'
	            and unlock_state=0
	           and unlock_date is not null 
	           and lock_date is not null
	and capacity_after_num>capacity_before_num
	group by user_guid
	,case when hour(unlock_date)>=6 and hour(unlock_date)<18 then '白' 
	         when hour(unlock_date)>=0 and hour(unlock_date)<6 then '晚' 
	         when hour(unlock_date)>=18 and hour(unlock_date)<24 then '晚'
	else '' end
	
	;
	
	#插入到正式表
	#8 一般情况下使用insert overwrite table，防止重复调度，支持重跑
	insert overwrite table ${table_name} partition (pt='${date}')
	select  a.date_pt
	          ,a.city_guid 
	          ,a.city_name
	          ,b.bike_cnt 
	from tmp.tmp_${table_name}_ride_${date} a
	left join tmp.tmp_${table_name}_bike_schdule_${date} b
	#9 多连接一个连接一行 
	on a.date_pt=b.date_pt
	#10 如果b表是分区表，分区写在on条件中
	      and a.city_guid=b.city_guid
	      and a.city_name=b.city_name
	union all
	select  a.date_pt
	          ,a.city_guid 
	          ,a.city_name
	          ,a.bike_cnt 
	from dw.dw_bike_total_amount a
	#11 a表有分区写在where 中
	where pt=${date_1}
	;
	
	-- 删除临时表
	#12 使用完后统一删除临时表
	drop table if exists tmp.tmp_${table_name}_ride_${date};
	
	"
	## hive脚本执行区
	hive_txt "$sql_1"