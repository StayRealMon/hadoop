# Join 从句 #
## 内连接 全外连接 左、右连接 交叉连接 ##

**Inner join --两个列的交集**
**Left Out join**，--LEFT JOIN结果中必包含坐标中的记录  操作索引（左表减去左右交集
**Right Out join **，-- RIGHT JOIN结果中必然包含右表中的记录
**Full join**  --可用UNION ALL 连接左右join 变为full join
**Cross join** –笛卡尔积 cartesian  叉乘 a×b


## JOIN 连接优化查询 ##
**Trick1**
Update a.x set a.x = x where a.x in (select b.x from a join b where a.x = b.x)
Update a join (select b.x from a join b on a.x = b.x) b on a.x = b.x set a.x = x
**Trick2**
Select a.x, a.y, (select b.z from b where b.z = a.z) from a
Select a.x , a.y, a.z from a left join b on a.x = b.x

## 数据库应用系统涉及三种模型 ##
**概念模型、逻辑模型和物理模型**
**需求分析**：确立系统所需要实现的功能模块
**概念设计**：设计E-R图
**逻辑设计**：E-R图转换成关系模式；创建数据库说明；数据模型的优化；设计用户子模式
**物理设计**：设计的具体的表，使用具体的数据库关系软件如MySQL

## 六种范式 ##
**第一范式-1NF**：关系模式的所有属性均为简单属性，即属性不可再分
**第二范式-2NF**：在第一范式的基础上，每个非主属性都完全依赖于关系模式的码，即消除非主属性对码的部分依赖；
**第三范式-3NF**：在第二范式的基础上，每个非主属性都不传递依赖于候选码，即消除非主属性对码的传递依赖；（非主属性仅依赖于主键）
**BC范式-BCNF**：所有属性都不传递依赖于关系的任何候选键。

## X&S LOCK ##
**X锁** - 写锁，在写之前谁都不能读写
**S锁** - 读锁，在读过之后，可读不可写

## 数据库语言 ##
**1.数据查询语言DQL**
数据查询语言DQL基本结构是由SELECT子句，FROM子句，WHERE子句组成的查询块：
SELECT <字段名表>
FROM <表或视图名>
WHERE <查询条件>
**2 .数据操纵语言DML**
数据操纵语言DML主要有三种形式：
1) 插入：INSERT
2) 更新：UPDATE
3) 删除：DELETE
**3. 数据定义语言DDL（数据库模式描述语言）**
数据定义语言DDL用来创建数据库中的各种对象-----表、视图、
索引、同义词、聚簇等如：
CREATE TABLE/VIEW/INDEX/SYN/CLUSTER
| | | | |
表 视图 索引 同义词 簇
DDL操作是隐性提交的！不能rollback
**4. 数据控制语言DCL**
数据控制语言DCL用来授予或回收访问数据库的某种特权，并控制
数据库操纵事务发生的时间及效果，对数据库实行监视等。如：
1) GRANT：授权。
2) ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。
回滚---ROLLBACK
回滚命令使数据库状态回到上次最后提交的状态。其格式为：
SQL>ROLLBACK;
3) COMMIT [WORK]：提交。

    在数据库的插入、删除和修改操作时，只有当事务在提交到数据库时才算完成。在事务提交前，只有操作数据库的这个人才能有权看到所做的事情，别人只有在最后提交完成后才可以看到。
    提交数据有三种类型：显式提交、隐式提交及自动提交。

## 关系数据模型 ##
**数据结构/操作集合/完整性约束**
完整性规则：实体完整性（Entity Integrity)主键不为空
参考完整性（Referential Integrity）外键在主键中有值
域完整性（Domain Integrity）
用户定义完整性（User defined Integrity）实际情况年龄大于0小于100

**原子性**：一个事务对数据库的所有操作，是一个不可分割的工作单元，这些操作要么全部执行，要么什么也不做（由DBMS的事务管理子系统来实现）；
**一致性**：一个事务独立执行的结果，应（由DBMS的完整性子系统执行测试任务）；
**隔离性**（由DBMS的并发控制子系统实现）；
**持久性**（由DBMS的恢复管理子系统实现的）

## 事务隔离级别 ##
 Read uncommittd、 Read committed、Repeatble read和Seriable  依次解决脏读、不可重复读和幻读
不可重复读表示两次执行同样的查询，可能会得到不一样的结果。
**READ UNCOMMITTED**（未提交读）：事务中的修改，即使没有提交，对其他事务也都是可见的。也被称为脏读。
**READ COMMITTED**（提交读）：一个事务开始时，只能看到已经提交的事务所做的修改。换句话说，一个事务从开始直到提交之前，所做的任何修改对其他事务都是不可见的。
**REPEATABLE READ**（可重复读）：该级别保证了在同一个事务中多次读取同样记录的结果是一致的。不能解决幻读的问题：即当某个事务在读取某个范围内的记录时，另外一个事务又在该范围内插入了新的记录，当之前的事务再次读取该范围内的记录时，会产生幻行。
**SERIALIZABLE**（可串行化）：强制事务串行执行。
