初学JDBC和MySQL，实现简陋的登录功能；

* 通过键盘录入用户名和密码
* 判断用户是否登录成功

<!--more-->

原理其实很简单：

把登陆的用户名和密码  用sql语句去数据库查询;  若有查询结果则证明登录成功， 反之。

查询语句:

```sql
select * from users where username='' and password='';
```

####首先创建用户数据表并插入几条数据：

```mysql
create table users(
	id int primary key auto_increment,
  username varchar(32),
  password varchar(32)
);

insert into users values(null, 'zhang', '123');
insert into users values(null, 'wang', '123');

```



#### 实现登陆的代码部分:

```java
package cn.coder.login;

import cn.utils.JDBCUtils;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

/**
 * 1.通过键盘录入用户名和密码
 * 2.判断用户是否登录成功
 */
public class Logindemo {
    Connection connection = null;
    Statement statement = null;
    ResultSet resultSet = null;

    public boolean login(String username, String password) {
        if (username == null || password == null) {
            return false;
        }
        try {
            connection = JDBCUtils.getConnection();
            statement = connection.createStatement();
            String sql = "select * from users where username='" + username + "'and password='" + password + "';";
            resultSet = statement.executeQuery(sql);
            // 如果有返回 则有下一行  resultSet.next();将返回true 否则返回false
            return resultSet.next();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.close(resultSet, statement, connection);
        }
        return false;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.println("-------请输入用户名：-------");
        String username = in.nextLine();
        System.out.println("-------请输入密码：-------");
        String password = in.nextLine();

        boolean login = new Logindemo().login(username, password);
        if (login) {
            System.out.println("登录成功！");
        } else {
            System.out.println("用户名或密码错误！");
        }
    }
}

```

#### JDBCUtils 工具包代码：

其中包括: (有详细注释)

* 加载properties配置文件的静态代码块

* 数据库的链接
* 释放资源的两个静态重载方法

```java
package cn.utils;

import java.io.FileReader;
import java.io.IOException;
import java.sql.*;
import java.util.Properties;

/**
 * JDBC工具类
 */
public class JDBCUtils {
    private static String url;
    private static String user;
    private static String pwd;
    private static String driver;

    static {
        // 静态代码块  只执行一次  可用于加载properties
        // properties 集合类  静态代码块不能抛出异常
        Properties properties = new Properties();
        try {
            // 获取src下的文件   ClassLoader -->  类加载器
            String path = JDBCUtils.class.getClassLoader().getResource("jdbc.properties").getPath();

            properties.load(new FileReader(path));
            url = properties.getProperty("url");
            user = properties.getProperty("user");
            pwd = properties.getProperty("password");
            driver = properties.getProperty("driver");

            Class.forName(driver); // 注册驱动 加载进内存
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    /**
     * 获取数据库链接对象
     *
     * @return
     */
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(url, user, pwd);
    }

    /**
     * 释放资源
     *
     * @param resultSet
     * @param statement
     * @param connection
     */
    public static void close(ResultSet resultSet, Statement statement, Connection connection) {
        if (resultSet != null) {
            try {
                resultSet.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (statement != null) {
            try {
                statement.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (connection != null) {
            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

}

```



相关的配置文件：

jdbc.properties

```properties
url=jdbc:mysql://localhost:3306/db1
user=root
password=root
driver=com.mysql.jdbc.Driver
```

