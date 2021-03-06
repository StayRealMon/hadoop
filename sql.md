### mysql面试题 ###
数据库索引，B树和B+树；索引的原理：b+树的好处，b+树和b树的区别
>为什么用B+树？因为节点存的数据多信息多能够高效地利用空间，提升查询速度

|@| 介绍一下索引，索引设置的规则，索引的最左前缀原则
> 唯一性索引找 **区分度高**的列建索引；**经常查询排序分组统计**的列建立索引；**数据量小**的列；尽量扩展索引 **rebuild**避免删除新建

```sql
-- 覆盖索引
alter table table_name add index index_name(col1,col2,col3);
explain select * from table_name where col1='' and col2 ='' and col3 =''
explain select * from table_name where col2 ='' and col3 =''
explain select * from table_name where col3='' and col1 =''
explain select col3 from table_name where col3='' and col1 =''

-- 建立索引的时候会建立一个index_name，但是show index 的时候会显示三个，三个index的Key_name都一样是index_name，但是按照建立顺序有Seq_in_index的区别之分，越小越靠前靠左
-- 实际查询的时候，若where条件之后没有最左的列col1，explain指标中type为all全表扫描
-- 若where条件之后有最左的列col1(但是顺序可以不按照建立索引的顺序，sql执行会先进行优化以用到索引)，此时一定会用到联合索引，type为ref，ref(显示索引的哪一列被用到了，一般为一个常量)可能达到const级别，possible_key和key会显示index_name表示用到了索引
-- 若select语句之后有明确说明查询列为索引中的列，此时type级别可能会达到index(index比all好一点，index是全索引扫描而all是表扫描)，possible_key可能会为null，key一般为索引名(因为用到了索引)，extra出了using where 会多一个using index，代表用到了索引进行扫描
```

|@| 聚簇索引和非聚簇索引的区别
> 1. 聚簇索引：将数据存储与索引放到了一块，找到索引也就找到了数据 **InnoDB**；非聚簇索引：将数据存储于索引分开结构 **MyISM**
> 2. 主键(自增)默认使用聚簇索引，只要索引是相邻的，那么对应的数据一定也是相邻地存放在磁盘上的。
> 3. 聚簇优势：访问同一数据页不同行记录时，已经把页加载到了Buffer中，再次访问的时候，会在内存中完成访问，**减少I/O**；适合用在排序的场合；适合取出一定范围数据；减少了当出现行移动或者数据页分裂时辅助索引的维护工作

![https://www.jianshu.com/p/fa8192853184](https://upload-images.jianshu.io/upload_images/10154499-d53a5ce9cecf22f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/864/format/webp)

|@| [explain优化指标](https://www.cnblogs.com/gdwkong/articles/8505125.html "explain优化指标")
> 1. table ：这一列是查询设计的表
> 2. type ：指标从好到坏依次是：system>const>eq_ref>ref(最好能达到，表示所有具有匹配的索引的行都被用到)>fulltext>ref_or_null>index_merge>unique_subquery>index_subquery>range(索引范围内查找)>index(全索引树扫描)>ALL(全表扫描)
> 3. rows:行数


# Join 从句 #
## 内连接 全外连接 左、右连接 交叉连接 ##
> **Inner join --两个列的交集**
> **Left Out join**，--LEFT JOIN结果中必包含坐标中的记录  操作索引（左表减去左右交集，即使右表中没有匹配，也从左表返回所有的行
> **Right Out join **，-- RIGHT JOIN结果中必然包含右表中的记录，即使左表中没有匹配，也从右表返回所有的行
> **Full join**  --可用UNION ALL 连接左右join 变为full join，只要其中一个表中存在匹配，就返回行
> **Cross join** –笛卡尔积 cartesian  叉乘 a×b

## 连接2.0 ##
> **内联接**（典型的联接运算，使用像 =  或 <之类的比较运算符）。包括 **相等联接**和 **自然联接**。     
> 内联接使用比较运算符根据每个表共有的列的值匹配两个表中的行。例如，检索 students和courses表中学生标识号相同的所有行。
> **外联接**。外联接可以是左向外联接、右向外联接或完整外部联接。在 FROM子句中指定外联接时，可以由下列几组关键字中的一组指定：     
> 1）LEFT  JOIN或LEFT OUTER JOIN     
> 左向外联接的结果集包括  LEFT OUTER子句中指定的左表的所有行，而不仅仅是联接列所匹配的行。如果左表的某行在右表中没有匹配行，则在相关联的结果集行中右表的所有选择列表列均为空值。       
> 2）RIGHT  JOIN 或 RIGHT  OUTER  JOIN     
> 右向外联接是左向外联接的反向联接。将返回右表的所有行。如果右表的某行在左表中没有匹配行，则将为左表返回空值。       
> 3）FULL  JOIN 或 FULL OUTER JOIN
> 完整外部联接返回左表和右表中的所有行。当某行在另一个表中没有匹配行时，则另一个表的选择列表列包含空值。如果表之间有匹配行，则整个结果集行包含基表的数据值。
> **交叉联接**返回左表中的所有行，左表中的每一行与右表中的所有行组合。交叉联接也称作笛卡尔积。    
> FROM 子句中的表或视图可通过内联接或完整外部联接按任意顺序指定；但是，用左或右向外联接指定表或视图时，表或视图的顺序很重要。有关使用左或右向外联接排列表的更多信息，请参见使用外联接。

## 等值&自然连接 ##
> 等值连接是从关系R和S的广义笛卡尔积中选取A和B“属性值”相等的元组，所以只要两个关系里面的有元祖属性值相等就可以进行。 
> 自然连接是要求R和S中有一个或者多个相同的属性组

## 启发式优化规则 ##
> 1. **选择运算尽可能早做**，在优化策略中这是最重要，最基本的一条，它常常可以使执行节约几个数量级，因为选择运算一般使计算的中间结果大大变小
> 2. 把 **投影运算和选择运算同时进行**。如果有若干的投影和选择运算，并且他们都对同一个关系进行操纵的话，就可以在扫描此关系的同时完成所有的这些运算以避免重复扫描关系。
> 3. 把 **投影同其前或其后的双目运算结合**起来，没有必要为了去掉某些字段而扫描一遍关系
> 4. 把某些 **选择同在他前面要执行的笛卡儿积结合**成一个连接运算，连接特别是等值连接运算要比同样关系上的笛卡儿积省很多时间
> 5. 找出 **公共子表达式**


## JOIN 连接优化查询 ##
```sql
    **Trick1**
    Update a.x set a.x = x where a.x in (select b.x from a join b where a.x = b.x)
    Update a join (select b.x from a join b on a.x = b.x) b on a.x = b.x set a.x = x
    **Trick2**
    Select a.x, a.y, (select b.z from b where b.z = a.z) from a
    Select a.x , a.y, a.z from a left join b on a.x = b.x
```

## MyISAM&Innodb ##
1. MyISAM引擎是一种非事务性(不支持事务)的引擎，提供高速存储和检索，以及全文搜索能力，适合数据仓库等`查询频繁`的应用。
2. MyISAM和Innodb的区别：两种类型最主要的差别就是Innodb支持事务处理与外键和行级锁。而MyISAM不支持行级锁仅支持表级锁。所以MyISAM往往就容易被人认为只适合在小项目中使用。


## 数据库应用系统涉及三种模型 ##
> **概念模型、逻辑模型和物理模型**
> 概念模型独立于具体的机器和DBMS
> 
> **需求分析**：确立系统所需要实现的功能模块
> **概念设计**：设计E-R图
> **逻辑设计**：需求概念转化为数据库逻辑模型；E-R图转换成关系模式；创建数据库说明；数据模型的优化；设计用户子模式
> **物理设计**：选择合适的DBMS，设计的具体的表、字段以及命名规范，使用具体的数据库关系软件如MySQL，反范式化设计

## 模式 ##
> **一、模式（Schema）**
> 定义：也称逻辑模式，是数据库中全体数据的逻辑结构和特征的描述，是所有用户的公共数据视图。
> 
>**二、外模式（External Schema）**
>定义：也称子模式（Subschema）或用户模式，是数据库用户（包括应用程序员和最终用户）能够看见和使用的局部数据的逻辑结构和特征的描述，是数据库用户的数据视图，是与某一应用有关的数据的逻辑表示。

>**三、内模式（Internal Schema）**
>定义：也称存储模式（Storage Schema），它是数据物理结构和存储方式的描述，是数据在数据库内部的表示方式（例如，记录的存储方式是顺序存储、按照B树结构存储还是按hash方 法存储；索引按照什么方式组织；数据是否压缩存储，是否加密；数据的存储记录结构有何规定）

> 概念模式，也称作模式
> 外模式，也称作逻辑模式
> 内模式，也称作物理模式

>所以逻辑数据独立性是指概念模式改变，外模式不改变


## 数据独立性 ##
> 数据独立性包括 **物理独立性**和 **逻辑独立性**。
>物理独立性指应用 **程序**与存储在磁盘的数据库中 **数据**相互独立，即数据物理存储改变时应用程序不变。
逻辑独立性指应用 **程序**与数据库 **逻辑**结构相互独立，即数据逻辑结构改变时，应用程序可以不变。

> 物理独立性：数据的物理存储改变，应用程序不用改变；
> 逻辑独立性：数据的逻辑结构改变，应用程序不用改变。

## 六种范式 ##
> **第一范式-1NF**：关系模式的所有属性均为简单属性，即属性不可再分
> **第二范式-2NF**：在第一范式的基础上，每个非主属性都完全依赖于关系模式的码，即消除非主属性对码的部分依赖；
> **第三范式-3NF**：在第二范式的基础上，每个非主属性都不传递依赖于候选码，即消除非主属性对码的传递依赖；（非主属性仅依赖于主键）
> **BC范式-BCNF**：所有属性都不传递依赖于关系的任何候选键。

> R 中的属性全部是主属性，则 R 的最高范式必定是

## 码 & 键 ##
> **候选码**：如果关系中的某一属性组的值能唯一地标识一个元祖，则称该属性组为候选码；
> **主码**：如果一个关系有多个候选码，则选定其中一个为主码；
> **主属性**：候选码的诸属性称为主属性；
> **非主属性**：不包含在任何候选码中的属性称为非主属性；


## X&S LOCK ##
> **X锁** - 写锁，在写之前谁都不能读写
> **S锁** - 读锁，在读过之后，可读不可写
> 就像操作系统中的读者和写着问题。要实现 **读读共享**、**读写互斥**、**写写互斥**。
> **S锁**只要有一个在读，就不允许写，而只要有一个在读，另一个就还可以读。
> **X锁**只要有一个再写，就不允许其他的读，也不允许其他的写。

## 封锁协议 ##
> **一级封锁协议**是：事务T在修改数据R之前必须先对其 **加X锁**，直到事务结束才释放。事务结束包括正常结束（COMMIT）和非正常结束（ROLLBACK）。
> 一级封锁协议可以 **防止丢失修改**，并保证事务T是可恢复的。使用一级封锁协议可以解决丢失修改问题。在一级封锁协议中，如果仅仅是读数据不对其进行修改，是不需要加锁的，它不能保证可重复读和不读“脏”数据。
> 
> **二级封锁协议**是：一级封锁协议加上事务T在读取数据R之前必须先对其 **加S锁**，读完后方可释放S锁。
> 二级封锁协议除防止了丢失修改，还可以进一步 **防止读“脏”数据**。但在二级封锁协议中，由于读完数据后即可释放S锁，所以它不能保证可重复读。
> 
> **三级封锁协议**是：一级封锁协议加上事务T在读取数据R之前必须先对其加S锁，直到事务结束才释放。
> 三级封锁协议除防止了丢失修改和不读“脏”数据外，还进一步防止了 **不可重复读**。
> 
> 上述三级协议的主要区别在于什么操作需要申请封锁，以及何时释放。
> 两段锁的根本概念：两段锁协议是指所有事务 **必须分两个阶段对数据项加锁和解锁**


## 数据库并发操作 ##
并发带来的数据不一致主要包括 **丢失修改**、**不可重复读**和 **读脏数据**
1. 丢失修改两个事务T1和T2读入同一数据并修改，**T2提交的结果破坏了T1提交的结果**，导致T1的修改被丢失。
2. 不可重复读 事务T1读取某一数据后，事务T2执行更新操作，使T1 **无法再现**前一次读取结果
3. 读“脏”数据是指事务T1修改某一数据，并将其写回磁盘，事务T2读取同一数据后，T1由于某种原因被 **撤销**，则T2读到的数据就是“脏”数据。

## 数据库恢复 ##
> 基础是利用转储的冗余数据。这些转储的冗余数据包括 **日志文件、数据库后备副本**
> 规范化过程主要为克服 **插入异常**，**更新异常**，**删除异常**和 **数据冗余**四个问题


## 数据库语言 ##
> **1.数据查询语言DQL**
> 数据查询语言DQL基本结构是由SELECT子句，FROM子句，WHERE子句组成的查询块：
> SELECT <字段名表>
> FROM <表或视图名>
> WHERE <查询条件>
> 
> **2 .数据操纵语言DML**
> 数据操纵语言DML主要有三种形式：插入：INSERT;更新：UPDATE;删除：DELETE
> 
> **3. 数据定义语言DDL（数据库模式描述语言）**
> 数据定义语言DDL用来创建数据库中的各种对象-----表、视图、
> 索引、同义词、聚簇等如：
> CREATE TABLE/VIEW/INDEX/SYN/CLUSTER
> | | | | |
> 表 视图 索引 同义词 簇
> DDL操作是隐性提交的！不能rollback
> 
> **4. 数据控制语言DCL**
> 数据控制语言DCL用来授予或回收访问数据库的某种特权，并控制
> 数据库操纵事务发生的时间及效果，对数据库实行监视等。如：GRANT：授权。ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。
> 回滚---ROLLBACK
> 回滚命令使数据库状态回到上次最后提交的状态。其格式为：
> SQL>ROLLBACK;COMMIT [WORK]：提交。
> 就像操作系统中的读者和写着问题。要实现读读共享、读写互斥、写写互斥。
> 只要有一个在读，就不允许写，而只要有一个在读，另一个就还可以读。
> 只要有一个再写，就不允许其他的读，也不允许其他的写。

```sql
    CREATE DATABASE my_db
    CREATE TABLE 表名称(列名称1 数据类型,列名称2 数据类型,
    ....
    )
```

## SQL执行顺序 ##
> 1、from子句组装来自不同数据源的数据；  
> 2、where子句基于指定的条件对记录行进行筛选；  
> 3、group by子句将数据划分为多个分组；  
> 4、使用聚集函数进行计算；  
> 5、使用having子句筛选分组；  
> 6、select计算所有的表达式；  
> 7、使用order by对结果集进行排序

## 关系代数 ##
> **关系运算**：选择、投影、连接、除
> **传统集合运算**：并、差、交、笛卡尔
> 5种**基本运算**：并、差、笛卡尔、选择、投影
> 
> 关系代数运算中的基本运算包括并(∪)、差(-)、广义笛卡尔积(×)、投影(π)和选择(σ)，其他运算的功能都可以由这五种基本运算来实现。

## 关系数据模型 ##
> **数据结构/操作集合/完整性约束**
> 完整性规则：实体完整性（Entity Integrity)主键不为空
> 参考完整性（Referential Integrity）外键在主键中有值
> 域完整性（Domain Integrity）
> 用户定义完整性（User defined Integrity）实际情况年龄大于0小于100
> 
> **原子性**：一个事务对数据库的所有操作，是一个不可分割的工作单元，这些操作要么全部执行，要么什么也不做（由DBMS的事务管理子系统来实现）；
> **一致性**：一个事务独立执行的结果，应（由DBMS的完整性子系统执行测试任务）；
> **隔离性**（由DBMS的并发控制子系统实现）；
> **持久性**（由DBMS的恢复管理子系统实现的）

> 数据的 **完整性**
> 防止数据库中存在 **不符合语义的数据**，也就是防止数据库中存在 **不正确的数据**
> 防范对象：不合语义的、不正确的数据
> 数据的 **安全性**
> 保护数据库 防止恶意的破坏和非法的存取
> 防范对象：**非法用户和非法操作**

## 事务隔离级别 ##
>  Read uncommittd、 Read committed、Repeatble read和Seriable  依次解决脏读、不可重复读和幻读
> 不可重复读表示两次执行同样的查询，可能会得到不一样的结果。
> **1. READ UNCOMMITTED**（未提交读）：事务中的修改，即使没有提交，对其他事务也都是可见的。也被称为脏读。
> **2. READ COMMITTED**（提交读）：一个事务开始时，只能看到已经提交的事务所做的修改。换句话说，一个事务从开始直到提交之前，所做的任何修改对其他事务都是不可见的。
> **3. REPEATABLE READ**（可重复读）：该级别保证了在同一个事务中多次读取同样记录的结果是一致的。不能解决幻读的问题：即当某个事务在读取某个范围内的记录时，另外一个事务又在该范围内插入了新的记录，当之前的事务再次读取该范围内的记录时，会产生幻行。
> **4. SERIALIZABLE**（可串行化）：强制事务串行执行。

## 事务隔离级别 ##
> **1. 未提交读(Read Uncommitted)**：允许脏读，也就是可能读取到其他会话中未提交事务修改的数据。
> **2. 提交读(Read Committed)**：只能读取到已经提交的数据。Oracle等多数数据库默认都是该级别 (不重复读)
> **3. 可重复读(Repeated Read)**：mysql默认级别。可重复读。在同一个事务内的查询都是事务开始时刻一致的，InnoDB默认级别。在SQL标准中，该隔离级别消除了不可重复读，但是还存在幻象读
> **4. 串行读(Serializable)**：完全串行化的读，每次读都需要获得表级共享锁，读写相互都会阻塞


## 高效查询 ##
> 应尽量避免在 where 子句中使用 or 来连接条件，否则将导致引擎放弃使用索引而进行全表扫描，如：  
> select id from t where num=10 or num=20  
> 可以这样查询：  
> select id from t where num=10  
> union all  
> select id from t where num=20
> 
> union和union all的区别是,union会自动压缩多个结果集合中的重复结果，而union all则将所有的结果全部显示出来，不管是不是重复。
> **UNION** 操作符用于合并两个或多个 SELECT 语句的结果集。请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。如果允许重复的值，请使用 UNION ALL。

## 故障 ##
> **1. 事务故障**是由于程序执行错误而引起事务非预期的、异常终止的故障。它发生在单个事务的局部范围内，实际上就是程序的故障。
> 事务故障更多的是非预期的，不能由事务程序处理的情况，主要有：
> - 逻辑上的错误，如运算溢出、死循环、非法操作、地址越界等等；
> - 违反完整性限制的无效的输入数据；
> - 违反安全性限制的存取权限；
> - 资源限定，如为了解除死锁、实施可串化的调度策略等而ABORT一个事务；
> - 用户的控制台命令。
> 
> **2. 系统故障**是指系统在运行过程中，由于某种原因，造成系统停止运行，以致事务在执行过程中以非正常的方式终止，致使内存中的信息丢失，而存储在外存上的数据未受影响。
> **3. 介质故障**是指外存储设备故障，主要有磁盘损坏，磁头碰撞盘面，突然的强磁场干扰，数据传输部件出错，磁盘控制器出错等。

## 函数 ##
> **sum()**:函数所处理的字段类型必须是数值型的，不能是其他数据类型的，比如字符或日期。
> **count()**:count（列） 统计中如果是null的话，是不计入统计的，所以用count(列)替换 count(*) 有可能会返回错误的结果
> **Max()**和 **Min()**可以用于字符型的列
> **avg()**这个是数值函数 , 不能 用于日期
> **where**用于对行的筛选，**having**用于对组的筛选

## 关系数据库三种基本操作 ##
> 关系数据库中定义了关系操作，关系操作的能力可用关系代数来表示，关系代数的运算可分两类：一类是传统的集合运算，如 **并、差、交、笛卡尔积** ，这类运算将关系看成元组的集合，其运算是从关系的“水平”方向，即行的角度来进行的。另一类是专门的关系运算，这类运算不仅涉及行，而且涉及列，主要包括对关系 **进行垂直分解的投影操作**，对关系 **进行水平分解的选择操作**，对关系 **进行结合的连接操作**，在关系数据库的任何检索操作都可以由三种基本检索运算组合而实现。

## 查询的步骤 ##
> 1. 客户端发送一条查询给服务器；
> 2. 服务器先会检查查询缓存 **query cache**，如果命中了缓存，则立即返回存储在缓存中的结果。否则进入下一阶段；
> 3. 服务器端进行SQL解析 **parsing**、预处理 **transition**，再由优化器 **optimization**生成对应的执行计划；
> 4. 根据优化器生成的执行计划，调用存储引擎的API来执行分布 **distribution**查询；
> 5. 将结果返回给客户端


## DBS&DBMS&DB ##
> DBS由数据库(数据)、DBMS(软件)、DBA(人员)、硬件平台(硬件)、软件平台5个部分构成。其中DBMS是数据库系统的核心，它负责数据库中的数据组织、数据操纵、数据维护、控制及保护和数据服务等工作。
>>DBS包括DBMS和DB

## 事务特点 ##
> **1. 原子性：**事务是一个不可分割的整体，为了保证事务的总体目标，事务必须具有原子性，即当数据修改时，要么全执行，要么全不执行，即不允许事务部分的完成，避免了只执行这些操作的一部分而带来的错误。原子性要求失误必须被完整执行。
> **2. 一致性：**一个事务执行之前和之后，数据库数据必须要保持一致性状态。数据库的一致性状态应该满足模式锁指定的约束，那么在完整执行该事务后数据库仍然处于一致性的状态。为了维护所有数据的完整性，在关系型数据库中，所有规则必须应用到事务的修改上。数据库的一致性状态由用户来负责，由并发控制机制实现。例如银行转账，转账前后两个账户金额之和应保持不变。由此并发操作带来的数据不一致性包括丢失数据修改、读脏数据。不可重复读、产生‘幽灵’数据。
> **3. 隔离性：**隔离性也被成为独立性,当两个或多个事务并发执行时，为了保证数据的安全性，将一个事物内部的操作与事务的操作隔离起来，不被其他正在执行的事务看到。
> **4. 持久性：**持久性也被成为永久性，事务完成之后，DBMS保证它对数据库中的数据的修改是永久性的，当系统或介质发生故障时，该修改也永久保持。持久性一般通过数据库备份与恢复来保证

## 模式、内模式、外模式 ##
> 1. **模式**又称概念模式或逻辑模式，对应于概念级。它是由数据库设计者综合所有用户的数据，按照统一的观点构造的全局逻辑结构，是对数据库中全部数据的逻辑结构和特征的总体描述，是所有用户的公共数据视图(全局视图)。它是由数据库管理系统提供的数据模式描述语言(Data Description Language，DDL)来描述、定义的，体现、反映了数据库系统的整体观。
> 2. **外模式**又称子模式或用户模式，对应于用户级。它是某个或某几个用户所看到的数据库的数据视图，是与某一应用有关的数据的逻辑表示。外模式是从模式导出的一个子集，包含模式中允许特定用户使用的那部分数据。用户可以通过外模式描述语言来描述、定义对应于用户的数据记录(外模式)，也可以利用数据操纵语言(Data Manipulation Language，DML)对这些数据记录进行。外模式反映了数据库的用户观。
> 3. **内模式**又称存储模式，对应于物理级，它是数据库中全体数据的内部表示或底层描述，是数据库最低一级的逻辑描述，它描述了数据在存储介质上的存储方式和物理结构，对应着实际存储在外存储介质上的数据库。内模式由内模式描述语言来描述、定义，它是数据库的存储观。


## JDBC驱动程序类型 ##
> 四种驱动方式：**jdbc-odbc桥接**、**本地API驱动**、**网络协议驱动**和**本地协议驱动**

> 1.   **JDBC-ODBC BRIDGE**
> 在JDBC出现的初期，JDBC-ODBC桥显然是非常有实用意义的，通过JDBC-ODBC桥，开发人员可以使用JDBC来存取ODBC数据源。不足的是，他需要在客户端安装ODBC驱动程序，换句话说，必须安装MICROSOFT WINDOWS的某个版本。使用这一类型你需要牺牲JDBC的平台独立性。另外，ODBC驱动程序还需要具有客户端的控制权限。
> 2.  **JDBC-NATIVE DRIVER BRIDGE** 　
> JDBC本地驱动程序桥提供了一种JDBC接口，它建立在本地数据库驱动程序的顶层，而不需要使用ODBC。 JDBC驱动程序将对数据库的API从标准的JDBC调用转换为本地调用。使用此类型需要牺牲JDBC的平台独立性，还要求在客户端安装一些本地代码。
> 3.  **JDBC-NETWORK BRIDGE** 
> JDBC网络桥驱动程序不再需要客户端数据库驱动程序。它使用网络上的中间服务器来存取数据库。这种应用使得以下技术的实现有了可能，这些技术包括负载均衡、连接缓冲池和数据缓存等。由于第3种类型往往只需要相对更少的下载时间，具有平台独立性，而且不需要在客户端安装并取得控制权，所以很适合于INTERNET上的应用。
> 4.   **PURE JAVA DRIVER**
>第4种类型通过使用一个纯JAVA数据库驱动程序来执行数据库的直接访问。此类型实际上在客户端实现了2层结构。要在N-层结构中应用，一个更好的做法是编写一个EJB，让它包含存取代码并提供一个对客户端具有数据库独立性的服务。 WEBLOGIC服务器为一些通常的数据库提供了JDBC驱动程序，包括ORACLE, SYBASE,MICROSOFT SQL SERVER以及INFORMIX。它也带有一种JDBC驱动程序用于CLOUDSCAPE，这是一种纯JAVA的DBMS，WEBLOGIC服务器中带有该数据库的评估版本。

## JDBC PreparedStatement ##
> PreparedStatement的一个缺点是，我们不能直接用它来执行in条件语句；需要执行IN条件语句的话，下面有一些解决方案：
>>1. 分别进行单条查询——这样做性能很差，不推荐。
>>2. 使用存储过程——这取决于数据库的实现，不是所有数据库都支持。
>>3. 动态生成PreparedStatement——这是个好办法，但是不能享受PreparedStatement的缓存带来的好处了。
>>4. 在PreparedStatement查询中使用NULL值——如果你知道输入变量的最大个数的话，这是个不错的办法，扩展一下还可以支持无限参数。

## 各式系统分类 ##
![各式系统](https://uploadfiles.nowcoder.com/images/20180513/4404901_1526174233409_F47CF3EEC871EB6DD4498CA2322CDDB5)
**一、表式系统**
仅支持关系（即表）数据结构，不支持关系（即集合）操作。 
**二、（最小）关系系统**
仅支持关系数据结构和三种关系搡作。即4.1.l中定义的关系系统。许多微机关系数据库系统如FoxBASE、FoxPro等就属于这一类。 
**三、关系完备的系统**
这类系统支持关系数据结构和所有的关系代数操作（功能上与关系代数等价）。 
**四、全关系系统**
这类系统支持关系模型的所有特征。即不仅是关系上完备的而且支持数据结构中域的概念，支持实体完整性和参照完整性。目前，大多数关系系统已不同程度上接近或达到了这个目标。

## mysql_db_query || mysql_query ##
1. mysql_db_query 成功返回资源号，失败返回FALSE；mysql_query成功返回TRUE,失败返回FALSE
2. mysql_db_query在功能上等于mysql_select_db() +mysql_query()
2. 不能用mysql_db_query函数临时在另一个数据库上执行sql语句，mysql_query可以

## BTREE索引和 HASH 索引 ##
>1.  HASH索引只用于使用 = 或 <=> 操作符的等式比较。如果一定要使用范围查询 的话，只能使用索引。
> 2. 优化器不能使用 Hash 索引来加速 order by 操作。
> 3. 使用 Hash 索引时 MySQL 不能确定在两个值之间大约有多少行。如果将一 个MyISAM表改为的 Hash 索引 memory 表，会影响一些查询的执行效率。
> 4. Hash索引只能使用整个关键字来搜索一行。

**HASH索引**：利用哈希函数，计算存储地址，检索时不需要像Btree那样，从根节点开始遍历，逐级查找。
1. 优点： 查找效率高。
2. 局限：仅仅满足=，in，<=>，查询，不能范围查询（原先有序的键值经过哈希函数运算，可能不再连续）；无法用于排序操作（order by）；当重复值时，效率并不比BTree高；不能利用部分索引键查询。
**BTREE索引**：Oracle数据库中最常见的索引类型是b-tree索引，也就是B-树索引
**位图索引(bitmap index)**：特定于该列只有几个枚举值的情况，比如性别字段，标示字段比如只有0和1的情况
**基于函数的索引**：经常对某个字段做查询的时候是带函数操作的，那么此时建一个函数索引就有价值了
**分区索引和全局索引**：用于分区表的时候。前者是分区内索引，后者是全表索引
**反向索引（REVERSE）**：（10001,10002,10033,10005,10016..）。这种情况默认索引分布过于密集，不能利用好服务器的并行，但是反向之后10001,20001,33001,50001,61001就有了一个很好的分布，能高效的利用好并行运算。

### 复合/组合索引 ###
复合索引在数据库操作期间所需的开销更小，可以代替多个单一索引；
```sql
create index idx1 on table1(col1,col2,col3)
```
窄索引是指索引列为1-2列的索引，宽索引也就是索引列超过2列的索引；优先级窄索引>宽索引
where子句查询的时候按照建立索引的顺序查询，否则会导致索引失效
有复合索引的时候就不要用单一索引，但是避免宽索引

## 索引失效或效率不高 ##
索引并不是越多越好，索引固然可以提高相应的 select 的效率，但同时也降低了 insert 及 update 的效率，因为 insert 或 update 时有可能会重建索引。
```sql
	#先删除原索引再手动创建；较为耗时
	drop index index_name;
	create index index_name on table_name (index_column);

	#直接重建索引；建议使用
	alter index indexname rebuild;
	alter index indexname rebuild online;
```
> rebuild是快速重建索引的一种有效的办法，因为它是一种使用现有索引项来重建新索引的方法。
> 
> 如果重建索引时有其他用户在对这个表操作，尽量使用带online参数来最大限度的减少索引重建时将会出现的任何加锁问题。

一个表的索引数最好不要超过6个

在where子句中'='的左边使用函数、算术运算或其他表达式运算，会导致索引失效
> 1. 使用了运算符!=，以及关键字not in, not exist等，认为产生的结果集很大，往往导致引擎不走索引而是走全盘扫描
> 2. 对索引字段使用了函数，如where substr(name, 1, 3)=‘mark’， 导致索引无效
> 3. 使用like和通配符，第一个字符是%将导致索引失效，如where name like "%ark“

## SQL优化 ##
1. 不要有超过5个以上的表连接（JOIN）;优先执行那些能够大量减少结果的连接
2. 考虑使用临时表或表变量存放中间结果
3. 少用子查询
4. 视图嵌套不要过深,一般视图嵌套不要超过2个为宜
5. 避免全表扫描，在where和orderby的列上建立index，高效地使用index
> 导致全表扫描的几种情况：
> 
> where is null，where中有为空的判断
> 
> where x != 0，where中有不等于和not in的判断
> 
> where name like '%abc%'，模糊查询时候第一个字符为% 
> 
> where substring(name,1,3) = ‘abc’，where中使用函数，会导致放弃索引导致全表扫描
> 
> where num/2 = 10 ，表达式会导致全表扫描，改为where num = 20
> 
> where num = @num，表达式中有参数，参数是在运行时被解析的，是在优化之后，因此会导致全表扫描
> 
> 在where中使用or连接字段的时候，若两个字段不全有索引会导致全表扫描；可以用union all连接or的两个条件的查询结果

6. 避免null，用数字0代替；null会占char(100)的空间不占varchar(100)的空间
7. update不要更新全部字段
8. 小表驱动大表用IN，大表驱动小表用EXISTS。IN适合的情况是外表数据量小的情况，而不是外表数据大的情况，因为 **IN会遍历外表的全部数据**，假设a表100条，b表10000条那么遍历次数就是100 * 10000次，而exists则是执行100次去判断a表中的数据是否在b表中存在，它只执行了a.length次数。至于哪一个效率高是要看情况的，因为 **in是在内存中比较的**，而 **exists则是进行数据库查询操作**的

## 触发器 ##
> 触发程序与表相关，当对表执行INSERT、DELETE或UPDATE语句时，将激活触发程序。可以将触发程序设置为在执行语句之前或之后激活。例如，可以在从表中删除每一行之前，或在更新了要想创建触发程序或舍弃触发程序，可使用CREATE TRIGGER或DROP TRIGGER语句
> 
> 触发程序不能调用将数据返回客户端的存储程序，也不能使用采用CALL语句的动态SQL（允许存储程序通过参数将数据返回触发程序）。
> 
> 使用OLD和NEW关键字，能够访问受触发程序影响的行中的列（OLD和NEW不区分大小写）。在INSERT触发程序中，仅能使用NEW.col_name，没有旧行。在DELETE触发程序中，仅能使用OLD.col_name，没有新行。在UPDATE触发程序中，可以使用OLD.col_name来引用更新前的某一行的列，也能使用NEW.col_name来引用更新后的行中的列。
> 
> 触发程序不能使用以显式或隐式方式开始或结束事务的语句，如START TRANSACTION、COMMIT或ROLLBACK

## 索引 ##
1. 索引可以分为唯一索引(建议用主键约束)、主键索引和聚集索引(最左原则)，而实现方式分为B+/散列/位图索引等
2. 索引把无序的数据变成有序的查询。先对创建索引的列进行排序，排序结果生成倒表，倒表内容中拼接上数据地址链，查询的时候先查倒排表取得地址链，再访问数据
3. B+数和hash树只是索引的数据结构和实现方式。B+树不像红黑树是二叉树，但是像红黑树一样保持平衡

### 原则 ###
> **索引在使用的时候要遵守最左原则**
> **索引在频繁查询的字段而不是频繁更新**
> **索引在区分度较高重复值较少的字段**
> **索引尽量扩展而不是新建**
> 索引维护也要空间并不是越多越好
> 删除大量数据前可以先删除索引提升维护速度

> BTREE索引和 HASH 索引的差异：
> 1. HASH索引只用于使用 = 或 <=操作符的等式比较。如果一定要使用范围查询 的话，只能使用BTREE索引。
> 2. 优化器不能使用 Hash 索引来加速 order by 操作。因为索引中存放的都是hash后的数字
> 3. 使用 Hash 索引时 MySQL 不能确定在两个值之间大约有多少行。如果将一 个MyISAM表改为的 Hash 索引 memory 表，会影响一些查询的执行效率。
> 4. Hash索引只能使用整个关键字来搜索一行
> 5. Hash索引遇到大量Hash值相等的情况后性能并不一定就会比B-Tree索引高。
> 
> HASH索引：利用哈希函数，计算存储地址，检索时不需要像Btree那样，从根节点开始遍历，逐级查找。 
> 优点： 查找效率高。
> 局限：仅仅满足=，in，<=>，IS (not) NULL查询，不能范围查询（原先有序的键值经过哈希函数运算，可能不再连续）;无法用于排序操作（order by）;当重复值时，效率并不比BTree高;不能利用部分索引键查询


## E-R图冲突 ##
> **属性冲突、命名冲突和结构冲突。**
> 属性冲突包括属性域冲突和属性取值单位冲突。
> 命名冲突包括同名异义和异名同义冲突。
> 结构冲突包括同一对象在不同应用中具有不同的抽象，同一实体在不同分E-R图中所包含的属性个数和属性排列次序不完全相同。

## 数据表删除 ##
> 1. 删除表中的数据以及定义(出手最狠)
> drop table Student；
> 2. 删除表中数据，定义还在(比较温柔)
> truncate table Student；
> 3. 删除表中所有数据，但是删的比较低效(温柔型)
> delete table Student；(系统一行一行删，保留日志，可以rollback)

## DELETE和TRUNCATE ##
> TRUNCATE TABLE比DELETE的速度快
> 1. 对于被外键约束的表，不能使用TRUNCATE TABLE，而应该使用不带WHERE语句的DELETE语句
> 2. 如果想保留标识计数值，要用DELETE，因为TRUNCATE TABLE会对新行标志符列使用的计数值重置为该列的种子
> 3. 在删除时如果遇到任何一行违反约束（主要是外键约束），TRUNCATE TABLE仍然删除，只是表的结构及其列、约束、索引等保持不变，但DELETE是直接返回错误

## 数据类型 ##
> **integer(size)，int(size)，smallint(size)，tinyint(size)**
> 仅容纳整数。在括号内规定数字的最大位数。
> **decimal(size,d)，numeric(size,d)**
> 容纳带有小数的数字。"size" 规定数字的最大位数。"d" 规定小数点右侧的最大位数。
> **char(size)**	
> 容纳固定长度的字符串（可容纳字母、数字以及特殊字符）。在括号中规定字符串的长度。
> **varchar(size)**	
> 容纳可变长度的字符串（可容纳字母、数字以及特殊的字符）。在括号中规定字符串的最大长度。
> **date(yyyymmdd)**	
> 容纳日期。
> 
> SELECT INTO语句从一个表中选取数据，然后把数据插入另一个表中。语句常用于创建表的备份复件或者用于对记录进行存档。

```sql
    select from where | group by | having | order by | limit
    
    SELECT DISTINCT Company FROM Orders
    SELECT * FROM Persons WHERE Year>1965
    SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William') AND LastName='Carter'
    SELECT * FROM Persons WHERE LastName IN ('Adams','Carter')
    SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC, OrderNumber ASC
    SELECT * FROM Persons WHERE LastName NOT BETWEEN 'Adams' AND 'Carter'
    SELECT LastName AS Family, FirstName AS Name
    FROM Persons as p
    
    SELECT * FROM Persons LIMIT 5
    SELECT TOP 50 PERCENT * FROM Persons
    SELECT * FROM Persons WHERE City NOT LIKE '_g%'
    //不以A或L或N开头的Person
    SELECT * FROM Persons WHERE City LIKE '[!ALN]%'
    
    INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
    UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing' WHERE LastName = 'Wilson'
    DELETE FROM Person WHERE LastName = 'Wilson'

    //创建时增加UNIQUE约束
    CREATE TABLE Persons(
    Id_P int NOT NULL PRIMARY KEY AUTO INCREMENT,

    City varchar(255) DEFAULT 'Sandnes',
    OrderDate date DEFAULT GETDATE(),

    FOREIGN KEY (Id_P) REFERENCES Persons(Id_P),
    CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName),

    CHECK (Id_P>0)
    )

    //修改&删除约束
    ALTER TABLE Persons
    ADD CONSTRAINT uc_PersonID UNIQU (Id_P,LastName)
    DROP CONSTRAINT uc_PersonID

    //在常常被搜索的列（以及表）上面创建索引
    CREATE UNIQUE INDEX index_name ON table_name (column_name DESC)


    //视图是基于 SQL 语句的结果集的可视化的表
    CREATE VIEW view_name AS
    SELECT column_name(s)
    FROM table_name
    WHERE condition

    //自带函数
    SELECT Customer,SUM(OrderPrice) FROM Orders GROUP BY Customer HAVING SUM(OrderPrice)<2000
    SELECT ProductName, UnitPrice, FORMAT(Now(),'YYYY-MM-DD') as PerDate FROM Products
```

## PostgreSQL ##
1. **特点：**跨平台；支持文本图像声音；多种编程接口；支持SQL多种功能子查询、外键、视图、多进程并发控制(MVCC)、异步复制等
2. 在PostgreSQL中，表可以设置为从“父”表继承其特征
3. PostgreSQL是第一个实现多版本并发控制（MVCC）功能的数据库管理系统，甚至在Oracle之前。MVCC功能在Oracle中称为快照隔离。
4. PostgreSQL是一个通用的对象 - 关系数据库管理系统。它允许您添加使用不同编程语言（如C / C ++，Java等）开发的自定义函数。
5. PostgreSQL旨在实现可扩展性。在PostgreSQL中，您可以定义自己的数据类型，索引类型，函数语言等。如果您不喜欢系统的任何部分，您可以随时开发自定义插件以增强它以满足您的要求，例如，添加新的优化。

### DATA Types ###

1. **Boolean**
2. **Character** types such as char(n), varchar(n), and text.
3. **Numeric** types such as integer and floating-point number.
4. **Temporal** types such as date, time, timestamp, and interval
5. **UUID** for storing Universally Unique Identifiers
6. **Array** for storing array strings, numbers, etc.
7. **JSON** stores JSON data
8. **hstore** stores key-value pair
9. **Special types** such as network address and geometric data.

> SMALLINT→(-32,768 to 32,767)；INT→(-2,147,483,648 to 2,147,483,647)；float(n)；numeric(p,s)
> DATE&TIME&TIMESTAMP&TIMESTAMPTZ(有时区)&INTERVAL(一段时间)
> JSONB二进制存储处理快插入慢，支持indexing
> UUID(Universal Unique Identifiers defined)国际化？URL脱敏？
> Special:box(a rectangular box)line(point set)point(a geometric pair of numbers)lseg(line segment)polygon(closed geometric)inet(IP4 address)macaddr(MAC address)
```

## PostgreSQL基本操作说明 ##
### 登陆 ###
跳板机+psql：psql [选项]... [数据库名称 [用户名称]]
```sql
	psql -h(ost) 10.111.50.54 -p(ort) 3438 -d(bname) tian -U(ser) tian
```

### 操作 ###
```sql
	//创建删除
	create/drop database tian;
	//查看、选择、退出数据库
	psql=# \l
	psql=# \c
	psql=# \q
	//查看表结构、大小
	psql=# \d + table_name
	psql=# \dt + table_name
	psql=# \timing	//timing模式下查看sql执行时间
	psql=# \x			//x模式下查看扩展模式显示查询结果
	psql=# \o file_name.csv	//导出文件
```