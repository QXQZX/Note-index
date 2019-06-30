登录：

```sql
mysql -u root -p
mysql-h ip -p
mysql —host=ip —user=root —password=
```

退出：

```
exit  ||  quit
```



查看数据库

```sql
show databases;
```



查看某个数据库的字符集：

​	show create database 数据库名称;

创建数据库：

​	create database db1;

​	create database if not exists db1;  # 如果不存在 创建db1



创建指定编码的 数据库：

​	create database db3 character set GBK;

​	create database if not exists db3 character set GBK;



修改数据库：

​	修改数据库的字符集：

​		alter database 数据库名称 character set 字符集名称;





删除数据库：

​	drop database 数据库名称;

​	drop database if exists 数据库名称;



使用数据库：

​	查询正在使用的数据库：	

​		select database();

​	使用数据库：

​		use 数据库名称;





操作表

​	create table 表名(

​		列名1 数据类型1,

​		列名2 数据类型2,

​		……

​		列名n 数据类型n   # 无逗号

​	);



​	show tables;   #  展示所有数据表

​	desc 表名;  # 查看表的结构

​	

创建数据表：

```mysql
create table student(

  id int PRIMARY KEY ,

  name varchar(32),

  age int,

  score double(4,1),

  birthday date,

  insert_time timestamp

);
```



删除数据表：

​	drop table 数据表名称;

​	drop table if exists 数据表名称;

复制数据表：

​	create table 表名 like 被复制的表名;



表的修改：

​	1.修改表名  alter table 表名 rename to 新的表名;

​	2.修改表的字符集  

​		show create table 表名; # 查看

​		alter table 表名 character set 字符集名称;

​	3.添加一列：

​		alter table 表名 add 列名 数据类型;

​	4.修改列的名称  类型

​		alter table 表名 change 列名 新列名 新数据类型;

​		alter table 表名 modify 列名 新数据类型;

​	4.删除列

​		alter table 表名 drop 列名;













​	