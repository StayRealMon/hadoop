# SQL × 50 #
1. Student(<u>**SId**</u>,Sname,Sage,Ssex)
SId 学生编号,Sname 学生姓名,Sage 出生年月,Ssex 学生性别
2. Course(<u>**CId**</u>,Cname,<u>*TId*</u>)
CId 课程编号,Cname 课程名称,TId 教师编号
3. Teacher(<u>**TId**</u>,Tname)
TId 教师编号,Tname 教师姓名
4. SC(<u>**SId,CId**</u>,score)
SId 学生编号,CId 课程编号,score 分数

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
    insert into Course values('01' , '语文' , '02');
    insert into Course values('02' , '数学' , '01');
    insert into Course values('03' , '英语' , '03');
        
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
- 查询同时存在" 01 “课程和” 02 "课程的情况
    select s.SId, sc1.score score-1, sc2.score score-2 
	from sc sc1 left join sc sc2 on sc1.SId = sc2.SId
	where sc1.CId = sc2.CId

    select * from 
	(select * from sc where sc.CId = '01') res1
	(select * from sc where sc.CId = '02') res2
	where res1.SId = res.SId
- 查询存在" 01 “课程但可能不存在” 02 "课程的情况(不存在时显示为 null )
    select * from
	(select * from sc where sc.CId = '01') res1
	 left join 
	(select * from sc where sc.CId = '02') res2 
	on res1.SId = res2.SId
- 查询不存在" 01 “课程但存在” 02 "课程的情况
    select * from sc sc1 join sc sc2 on sc1.SId = sc2.SId
	where sc1.SId not in 
	(select SId from sc where sc.CId = '01')
	and sc2.CId = '02'
- 查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩
