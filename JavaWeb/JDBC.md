### JDBC概念

 Java DataBase Connectivity       java操作数据库

JDBC的本质：  其实是sun公司定义的一套操作所有关系型数据库的准则(接口)。由各个数据库厂商去实现这套接口(写这套接口的实现类)，提供数据库驱动的jar包。我们可以使用这套JDBC接口编程，而真正执行的代码是驱动jar包中的实现类

```java
/*jar包中有Worker类； 官方Person接口*/
Person person = new Worker();   
person.eat(); // 直接调用的是Woker实现类的方法 
```

### 快速入门



#### 1.导入驱动jar包

自行去官网下载



#### 2.注册驱动

```java
static void registerDriver(Driver driver) //注册与给定的驱动程序 DriverManager 。
```

这句其实不用写，因为com.mysql.jdbc.Driver类中有静态代码块

```java
// com.mysql.jdbc.Driver类中有静态代码块
static {
  try {
    DriverManager.registerDriver(new Driver());
  } catch (SQLException var1) {
    throw new RuntimeException("Can't register driver!");
  }
}
```

所以在使用`Class.forName("com.mysql.jdbc.Driver");`  这一行代码加载类的同时，  已经自动的使用它内部的隐藏代码`DriverManager.registerDriver()`方法注册了驱动；



#### 3.获取数据库链接驱动  connection

```java
static Connection	getConnection(String url, String user, String password)
//尝试建立与给定数据库URL的连接。
/*
URL : 语法：jdbc:mysql://ip地址(域名):端口号/数据库名称
user : 
pwd : 
注：
jdbc:mysql://localhost:3306/xxx
locahost:3306可以省略
*/
```

Connection 数据库连接对象的功能：

```java
// 执行sql对象
Statement	createStatement() // 创建一个 Statement对象，用于将SQL语句发送到数据库。
PreparedStatement	prepareStatement(String sql, String[] columnNames)
// 创建一个默认的 PreparedStatement对象，能够返回给定数组指定的自动生成的键

// 管理实务
开启事务：void	setAutoCommit(boolean autoCommit) // 将此连接的自动提交模式设置为给定状态。
提交事务：void	commit() // 使自上次提交/回滚以来所做的所有更改都将永久性，并释放此 Connection对象当前持有的任何数据库锁。
回滚事务：void	rollback() // 撤消在当前事务中所做的所有更改，并释放此 Connection对象当前持有的任何数据库锁。
```



#### 4.定义sql

```java
String sql = "select * from xxx";
```



#### 5.获取执行sql语句的对象  Statement

**Statement对象 ：**  用于执行静态SQL语句并返回其生成的结果的对象。

```java
boolean	execute(String sql) // 执行给定的SQL语句，这可能会返回多个结果。(了解  不常用)
int	executeUpdate(String sql) // 执行给定的SQL语句，这可能是 INSERT ， UPDATE ，或 DELETE语句，或者不返回任何内容，如SQL DDL DML语句的SQL语句。
// 但会影响的行数 ：  可以用于判断是否执行成功
  
ResultSet	executeQuery(String sql) // 执行给定的SQL语句(DQL)，该语句返回单个 ResultSet对象。
```

**PrepareStatement 对象：**表示预编译的SQL语句的对象。可用于解决sql注入问题

静态的sql语句容易发生sql注入问题 如密码：a' or 'a' = 'a'

定义sql： sql参数的使用 ? 作为占位符  如 ` select * from user where username = ? password = ?;`

```java
PreparedStatement	connection.prepareStatement(String sql, String[] columnNames)
// 给？赋值
setXxx(参数1, 参数2) // 参数1 代表位置编号的位置 从1开始； 参数2，替换占位的值

```

注意：开发只会使用PrepareStatement来完成增删改查的所有操作，可以防止sql注入  效率更高

#### 6.执行sql  接受返回结果

ResultSet对象：

```java
boolean	next() // 将光标从当前位置向前移动一行。
String	getString(int columnIndex) // 这个检索的当前行中指定列的值 ResultSet对象为 String的Java编程语言。
String	getString(String columnLabel) // 这个检索的当前行中指定列的值 ResultSet对象为 String的Java编程语言。
  .......
```

#### 7.处理结果释放资源

```java
resultSet.close();
statement.close();
connection.close();
```



--------



### JDBC管理实务

1.事务：一个包含多个步骤的业务操作。如果这个业务被事务所管理，则这个步骤要么同时成功要么失败

2.使用connection对象来管理实务

* 开启事务：setAutoCommit(boolean autoCommit) // 在执行sql之前开启事务
* 提交事务：commit() // 当所有sql执行成功  提交事务
* 回滚事务：rollback() // 在catch中回滚事务



### 拓展的知识：

获取src下的路径文件的方式 —>ClassLoader 类加载器

```java
ClassLoader classLoader = JDBCUtils.class.getClassLoader();
URL res = classLoader.getResource("jdbc.properties");
String path = res.getPath();
// 链式写法
String path = JDBCUtils.class.getClassLoader().getResource("jdbc.properties").getPath();
```







