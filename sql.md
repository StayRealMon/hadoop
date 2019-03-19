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
