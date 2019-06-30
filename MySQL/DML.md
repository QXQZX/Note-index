### DML 增删表中的数据



1.添加数据(字符串用  '  ' ) 

​	insert into 表名(列名1，列名2。。。。) values(值1，值2.。。。。);

2.给所有的列添加

​	insert into 表名 values(值1，值2.。。。。);

3.删除数据

​	delete from 表名 [where 条件];

​	delete from 表名;  # 不推荐使用  数据量未知

​	truncate table 表名;    # 删除表  然后在创建一个一模一样的空表

4.修改数据

​	update 表名 set 列名1 = 值1, ....列名n = 值n where 条件;

​	如果不加where 条件将会更改所有的数据