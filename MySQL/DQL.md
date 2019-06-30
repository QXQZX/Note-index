### DQL:查询语句

1.排序查询

​		order by 排序字段1 排序方式1, 排序字段2 排序方式2..........;

​		ASC 升序  默认的

​		DESC 降序

​		多排序条件  依次使用



2.聚合函数

​	1.count  # 计算个数

​		一般选主键

​	2.max & min

​	3.sum

​	4.avg  平均值

​		select count(ifnull(,)) from 表名;

​			ifnull(列名,0)  把一列的中的null换成0



3.分组查询

​	select from 组名 group by 分组字段;

​	select          sex, avg(math), count(id)      from student     group by       sex;



where   having 的区别;

​		where 在分组之前筛选  如果不满足条件，则不参与分组.    =having   在分组之后进行筛选（面试常考）

​		where 后面不能跟聚合函数   having 可以进行聚合函数的判断



4.分页查询

​	limit 开始的索引，每页查询的条数;

​	select * from 表名 limit 0,3;





2.约束

3.多表之间的关系

4.范式

5.数据库的备份和还原



查询表中的数据

select * from 表名;

​		语法

​			select 

​					字段列表

​			from

​					表名列表

​			where

​					条件列表

​			group by 

​					分组之后的条件

​			order by

​					排序

​			limit 

​					分页限定;

​	

​	2.基础查询

​		select            name, math, eng, ifnull(math,0) + ifnull(eng, 0) as sum            from student; # 筛选时并计算（只有四则运算）

​		#  将筛选出 name   math  eng   sum  四列



​		进阶

​			select            name 名字, math 数学, eng 英语, ifnull(math,0) + ifnull(eng, 0) 总分            from student; 

​			将筛选出 name   math  eng   sum  四列  并重命名为  名字  数学........



3.条件查询

1.where 字句后面跟条件 >=  == != .......



4.模糊查询

​	like

​	站位符： _单个任意字符 "___" 是三个字符的 

​	 %多个任意字符  "%2324%"    包含2324的