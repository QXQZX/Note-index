1.数据库链接池

概念：其实就是一个容器(集合)，存放数据库链接的容器

当系统初始化好后，容器被创建，容器中会申请一些链接对象，当用户来访问数据库时，从容器中获取链接对象，用户访问完后，会将连接对象归还给容器。

好处：节约资源  用户访问高效

2.实现

​	标准接口：  DataSource  

```
获取连接方法 
getConnection()
归还连接方法
Connection.close() 如果连接对象connection是从连接池获取的 那么Conection.close()方法归还给连接池 而不是关闭
```

由数据库厂商来实现

C3P0：数据库链接池技术  

配置文件   properties和xml两种形式的

Druid：数据库连接池技术，由阿里巴巴提供的

步骤：

​	1.导入jar包

​	2.定义配置文件   <1>是properties形式的；<2>可以任意的名称 放在任意的目录下

​	3.加载配置文件

​	4.获取数据库链接对象 ：通过工厂类获取   DruidDataSourceFactory

​	4.获取连接 getConnection()





3.Spring JDBC

Spring框架是对JDBC的简单封装  提供了一个JDBCTemplate对象简化JDBC的开发

步骤：

1.导入jar包

2.创建JDBCTemplate对象  依赖于数据源的DataSource

JDBCTemplate template = new JdbcTemplate(ds);

3.调用JdbcTemplate的方法来完成CRUD的操作：

* update()  ：  执行DML语句 增删改查

* queryForMap() : 查询结果封装为 map集合      只能查一条；列名key  值value

* queryForList() : 查询集合封装为 List集合       将每一条记录封装为map集合 再将map封装成list

* query() : 查询结果  将结果封装为JavaBean对象     参数：(sql,  参数2)

  关于参数2：

  ```java
  List<Emp> list = template.query(sql, new BeanPropertyRowMapper<Emp>(Emp.class));
  new BeanPropertyRowMapper<Emp>(Emp.class) // JavaBean的自动封装
  ```

* queryForObject() : 将结果封装为对象  一般用于聚合函数的查询



