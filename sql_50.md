## 分组排名 ##
> 求每个班级的前两名

	select sid from 
		(select count(sc1.SId) as cout, sc1.SId as sid from yuewen_sc as sc1 join yuewen_sc as sc2
		on sc1.class = sc2.class and sc1.Score>sc2.Score
		group by sc.SId) as tmp
	where cout>1; 

# SQL × 50 #
1. Student(<u>**SId**</u>,Sname,Sage,Ssex)
SId 学生编号,Sname 学生姓名,Sage 出生年月,Ssex 学生性别
2. Course(<u>**CId**</u>,Cname,<u>*TId*</u>)
CId 课程编号,Cname 课程名称,TId 教师编号
3. Teacher(<u>**TId**</u>,Tname)
TId 教师编号,Tname 教师姓名
4. SC(<u>**SId,CId**</u>,score)
SId 学生编号,CId 课程编号,score 分数

		insert into Student values('01' , 'ZHAO' , '1990-01-01' , 'male');
		insert into Student values('02' , 'QIAN' , '1990-12-21' , 'male');
		insert into Student values('03' , 'SUN' , '1990-12-20' , 'male');
		insert into Student values('04' , 'LI' , '1990-12-06' , 'male');
		insert into Student values('05' , 'ZHOU' , '1991-12-01' , 'Female');
		insert into Student values('06' , 'WU' , '1992-01-01' , 'Female');
		insert into Student values('07' , 'ZHENG' , '1989-01-01' , 'Female');
		insert into Student values('09' , 'ZHANG' , '2017-12-20' , 'Female');
		insert into Student values('10' , 'LI' , '2017-12-25' , 'Female');
		insert into Student values('11' , 'LI' , '2012-06-06' , 'Female');
		insert into Student values('12' , 'ZHAO' , '2013-06-13' , 'Female');
		insert into Student values('13' , 'SUN' , '2014-06-01' , 'Female');

		create table Student(SId varchar(10),Sname varchar(10),Sage datetime,Ssex varchar(10));
		insert into Student values('01' , '赵雷' , '1990-01-01' , '男');
		insert into Student values('02' , '钱电' , '1990-12-21' , '男');
		insert into Student values('03' , '孙风' , '1990-12-20' , '男');
		insert into Student values('04' , '李云' , '1990-12-06' , '男');
		insert into Student values('05' , '周梅' , '1991-12-01' , '女');
		insert into Student values('06' , '吴兰' , '1992-01-01' , '女');
		insert into Student values('07' , '郑竹' , '1989-01-01' , '女');
		insert into Student values('09' , '张三' , '2017-12-20' , '女');
		insert into Student values('10' , '李四' , '2017-12-25' , '女');
		insert into Student values('11' , '李四' , '2012-06-06' , '女');
		insert into Student values('12' , '赵六' , '2013-06-13' , '女');
		insert into Student values('13' , '孙七' , '2014-06-01' , '女');
		
		 create table Course(CId varchar(10),Cname nvarchar(10),TId varchar(10));
		 insert into Course values('01' , 'Chinese' , '02');
		 insert into Course values('02' , 'Math' , '01');
		 insert into Course values('03' , 'English' , '03');

		create table Course(CId varchar(10),Cname nvarchar(10),TId varchar(10));
		insert into Course values('01' , '语文' , '02');
		insert into Course values('02' , '数学' , '01');
		insert into Course values('03' , '英语' , '03');
		    

	create table Teacher(TId varchar(10),Tname varchar(10));
	insert into Teacher values('01' , 'ZHANGSAN');
	insert into Teacher values('02' , 'LISI');
	insert into Teacher values('03' , 'WANGWU');

		create table Teacher(TId varchar(10),Tname varchar(10));
		insert into Teacher values('01' , '张三');
		insert into Teacher values('02' , '李四');
		insert into Teacher values('03' , '王五');
		
		create table SC(SId varchar(10),CId varchar(10),score decimal(18,1));
		insert into SC values('01' , '01' , 80);
		insert into SC values('01' , '02' , 90);
		insert into SC values('01' , '03' , 99);
		insert into SC values('02' , '01' , 70);
		insert into SC values('02' , '02' , 60);
		insert into SC values('02' , '03' , 80);
		insert into SC values('03' , '01' , 80);
		insert into SC values('03' , '02' , 80);
		insert into SC values('03' , '03' , 80);
		insert into SC values('04' , '01' , 50);
		insert into SC values('04' , '02' , 30);
		insert into SC values('04' , '03' , 20);
		insert into SC values('05' , '01' , 76);
		insert into SC values('05' , '02' , 87);
		insert into SC values('06' , '01' , 31);
		insert into SC values('06' , '03' , 34);
		insert into SC values('07' , '02' , 89);
		insert into SC values('07' , '03' , 98);

- 查询" 01 “课程比” 02 "课程成绩高的学生的信息及课程分数
	
		select * from (
		select s1.SId, s1.Sscore score-1, s2.Sscore score-2 
		from SC s1 left join SC s2 on s1.SId = s2.SId
		where s1.CId = '01' and s2.CId = '02' and s1.score > s2.score
		) res left join Student s on res.SId = s.SId

		 SELECT SId_res SId,  score_1, score_2, Sname, Sage, Ssex
		FROM (SELECT sc1.SId SId_res, sc1.score score_1, sc2.score score_2
			FROM test_SC sc1 LEFT JOIN test_SC sc2 ON  sc1.SId = sc2.SId
			where sc1.score > sc2.score and sc1.CId = '01' and sc2.CId = '02') 
			as tmp_res LEFT JOIN test_Student s on tmp_res.SId_res = s.SId

## QUESTION ##
- 查询同时存在" 01 “课程和” 02 "课程的情况
		select s.SId, sc1.score score-1, sc2.score score-2 
		from sc sc1 left join sc sc2 on sc1.SId = sc2.SId
		where sc1.CId = sc2.CId
		
		select * from 
		(select * from sc where sc.CId = '01') res1
		(select * from sc where sc.CId = '02') res2
		where res1.SId = res.SId
		
		SELECT SId_res SId, CId_res1 CId1, score_1 score1, CId_res2 CId2, score_2 score2, Sname, Sage, Ssex
		FROM (SELECT sc1.SId SId_res, sc1.CId CId_res1, sc1.score score_1, sc2.CId CId_res2, sc2.score score_2, sc1.CId CId_res
		FROM test_SC sc1 LEFT JOIN test_SC sc2 ON  sc1.SId = sc2.SId
		where sc1.CId = '01' AND sc2.CId = '02') 
		as tmp_res LEFT JOIN test_Student s on tmp_res.SId_res = s.SId
- 查询存在" 01 “课程但可能不存在” 02 "课程的情况(不存在时显示为 null )
		select * from 
		(select * from test_SC  where CId = '01')  t1 left JOIN 
		(select * from test_SC WHERE CId = '02') t2
		on t1.SId = t2.SId;
- 查询不存在" 01 “课程但存在” 02 "课程的情况
		select * from sc sc1 join sc sc2 on sc1.SId = sc2.SId
		where sc1.SId not in 
		(select SId from sc where sc.CId = '01')
		and sc2.CId = '02'
		
		select  res2.SId, res2.CId, res2.Score from 
		(select * from test_SC WHERE CId = '02' and SId not in 
		(select SId from test_SC where CId ='01')
		) res2 
- 查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩
		select stu.SId, stu.Sname, avg_score 
		FROM test_Student stu RIGHT JOIN 
		(SELECT SId, AVG(Score) avg_score from test_SC GROUP BY SId HAVING AVG(Score)>60) res 
		on res.SId = stu.SId ;


- 查询在 SC 表存在成绩的学生信息
		select * FROM test_Student WHERE SId in 
		(SELECT DISTINCT SId from test_SC sc WHERE sc.Score is NOT NULL);

- 查询所有同学的学生编号、学生姓名、选课总数、所有课程的成绩总和
		select stu.SId, Sname, res.cont, res.avge FROM test_Student stu LEFT JOIN
		(SELECT SId, COUNT(*) cont, SUM(Score) avge FROM test_SC GROUP BY SId)res ON stu.SId = res.SId;

- 查询「李」姓老师的数量
		select Tname, COUNT(*) amount FROM test_Teacher 	WHERE Tname LIKE '李%';

- 查询学过「张三」老师授课的同学的信息
		select * FROM test_Student stu WHERE SId in
		(SELECT SId from test_SC sc WHERE CId in
		(SELECT CId from test_Teacher te WHERE TId in
		(SELECT TId FROM test_Teacher WHERE Tname = '张三')));

		select stu.* FROM test_Student stu 
		INNER JOIN test_SC sc on sc.SId = stu.SId
		INNER JOIN test_Course co on co.CId = sc.CId
		INNER JOIN test_Teacher te on te.TId = co.TId
		WHERE Tname = '张三';


- 查询没有学全所有课程的同学的信息

		select stu.* FROM test_Student stu WHERE stu.SId in
		(SELECT SId FROM test_SC GROUP BY SId 
		HAVING COUNT(*)>=(SELECT COUNT(*)FROM test_Course));

- 查询至少有一门课与学号为" 01 "的同学所学相同的同学的信息
		SELECT stu.* from test_SC sc2 INNER JOIN test_Student stu on stu.SId = sc2.SId 
		where sc2.CId NOT in (SELECT sc1.CId from test_SC sc1 where sc1.SId='07');


- 查询和" 01 "号的同学学习的课程完全相同的其他同学的信息



- 查询没学过"张三"老师讲授的任一门课程的学生姓名

		SELECT stu.Sname from test_Student stu 
		WHERE stu.SId not in 
		(SELECT sc.SId from test_SC sc INNER JOIN test_Course co on co.CId = sc.CId
		INNER JOIN test_Teacher te on te.TId = co.TId WHERE te.Tname = '张三')

- 查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩

		SELECT stu.SId, stu.Sname, AVG(sc.Score) avge from test_Student stu 
		INNER JOIN test_SC sc ON stu.SId = sc.SId
		WHERE sc.Score < 60
		GROUP BY sc.SId
		HAVING COUNT(*) > 1

- 检索" 01 "课程分数小于 60，按分数降序排列的学生信息

		SELECT stu.* ,res.Score from test_Student stu 
		INNER JOIN (SELECT SId, Score from test_SC sc WHERE Score<60 and CId = '01')res
		ON res.SId = stu.SId ORDER BY Score DESC

- 按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩

		select res1.CId,Cname,cont,ma,mi,avge,notbad,okay,good,best FROM 
		(SELECT CId, AVG(Score) avge ,COUNT(*)cont,MAX(Score) ma,MIN(Score) mi, 
		COUNT(CASE WHEN sc.Score>=60 THEN 1 ELSE NULL END)/COUNT(sc.SId) notbad,
		COUNT(CASE WHEN sc.Score>=70 and sc.Score<80  THEN 1 ELSE NULL END)/COUNT(sc.SId) okay,
		COUNT(CASE WHEN sc.Score>=80 and sc.Score<90  THEN 1 ELSE NULL END)/COUNT(sc.SId) good,
		COUNT(CASE WHEN sc.Score>=90 and sc.Score<100  THEN 1 ELSE NULL END)/COUNT(sc.SId) best
		from test_SC sc GROUP BY CId ORDER BY avge DESC)res1
		LEFT JOIN test_Course cour on cour.CId = res1.CId

- 查询各科成绩最高分、最低分和平均分

## Sql排名和分组排名 ##
> select a.*, @lastType := @temp, @temp := a.type, if(@lastType = @temp,@rank:= @rank + 1,@rank := 1) as rank 
> from test a, (select @a := 0,@temp := 0,@rank :=0) b order by type,score;

## LIMIT &OFFSET##
 LIMIT 和 OFFSET 关键字。LIMIT 后的数字代表返回几条记录，OFFSET 后的数字代表从第几条记录开始返回（第一条记录序号为0），也可理解为跳过多少条记录后开始返回.

	SELECT * FROM employees LIMIT 5 OFFSET 5

在 LIMIT X,Y 中，Y代表返回几条记录，X代表从第几条记录开始返回（第一条记录序号为0），切勿记反

	SELECT * FROM employees LIMIT 5,5

## 截取函数 ##
substr(X,Y,Z) 或 substr(X,Y) 函数的使用。
其中X是要截取的字符串。
Y是字符串的起始位置（注意第一个字符的位置为1，而不为0），取值范围是±(1~length(X))，当Y等于length(X)时，则截取最后一个字符；当Y等于负整数-n时，则从倒数第n个字符处截取。
Z是要截取字符串的长度，取值范围是正整数，若Z省略，则从Y处一直截取到字符串末尾；若Z大于剩下的字符串长度，也是截取到字符串末尾为止。

	SELECT first_name FROM employees ORDER BY substr(first_name,length(first_name)-1)
	SELECT first_name FROM employees ORDER BY substr(first_name,-2)

## 聚合函数group_concat(X,Y) ##
SQLite的聚合函数group_concat(X,Y)，其中X是要连接的字段，Y是连接时用的符号，可省略，默认为逗号。此函数必须与 GROUP BY 配合使用。

	SELECT dept_no, group_concat(emp_no) AS employees
	FROM dept_emp GROUP BY dept_no

## CONCAT() ##
MySQL的Concat函数，CONCAT(str1,str2,...) as con
SQLLite，字符串连接用 ||

	select concat(last_name , "'" , first_name) as name from employees
	select (last_name || "'" || first_name) as name from employees

## DATEDIFF() ##
DATEDIFF是两个日期的天数差集。
datediff(@today,@yesterday) = 1
	SELECT a.id AS 'Id' FROM Weather a JOIN Weather b ON DATEDIFF(a.RecordDate, b.RecordDate) = 1 AND a.Temperature > b.Temperature;

## DISTINCT&GROUP BY 去重性能比较 ##
数据量非常巨大时候，比如1000万中有300W重复数据，这时候的distinct的效率低于group by；
对于相对重复量较小的数据量比如1000万中1万的重复量，用groupby的性能会低于distnct

	select distinct salary from salaries where to_date='9999-01-01' order by salary desc;


## CASE & DECODE ##
case用法： 
case a when **cond1** then **exp1** else **cond2** then **exp2** else **exp3** end
当a满足条件cond1时， 返回exp1；当a满足条件cond2时， 返回exp2；否则 返回exp3
交换性别：

	UPDATE salary SET sex = IF(sex = 'm','f','m');

交换座位：

	select (case 
	when mod(id,2)=1 and id = (select count(*)from seat) then id
	when mod(id,2)=0 then id-1
	else id+1
	end) as id,student from seat order by id;

**DECODE**函数适合多值等值查询
查询T_USER中的成绩 t_score 中成绩为65,95,73的记录显示为‘YES’否则显示"NO"。

	select u_id , u_name , u_score , decode(u_score,
       65, 'YES',
       95, 'YES',
       73, 'YES',
	'NO') 
	from T_USER ;


##IF&IFNULL&NULLIF##
**IF( expr1 , expr2 , expr3 )**
SELECT IF(FALSE,1+1,1+2);
select *,if(book_name='java','已卖完','有货') as product_status from book where price =50

**IFNULL( expr1 , expr2 )**
SELECT IFNULL(NULL,"11");	res-> 11
SELECT IFNULL("00","11");	res-> 00

**NULLIF(expr1,expr2)**：如果两个参数相等则返回NULL，否则返回第一个参数的值expr1
select nullif(1,1)	res->null
selectnullif(123,321);res->123

## Row_number() ##
Row_number() over ((partition by col1) order by col2 (asc/desc)) as rank
先根据col1对表进行分组，再根据col2进行分组排序，返回排序编号
如 

	Row_number(partition by dept order by salary desc ) as rank

返回按照部门中的工资进行降序排序的排名