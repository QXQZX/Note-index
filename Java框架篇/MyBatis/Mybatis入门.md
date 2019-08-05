###  MyBatis

MyBatis 本是[apache](http://baike.baidu.com/view/28283.htm)的一个开源项目[iBatis](http://baike.baidu.com/view/628102.htm), 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis，实质上Mybatis对ibatis进行一些改进。 

MyBatis是一个优秀的持久层框架，它对jdbc的操作数据库的过程进行封装，使开发者只需要关注 SQL 本身，而不需要花费精力去处理例如注册驱动、创建connection、创建statement、手动设置参数、结果集检索等jdbc繁杂的过程代码。

对jdbc的封装框架有哪些：Hibernate,dbutils,jdbcTemplate[spring]，mybatis

原理：Mybatis通过**xml或注解**的方式将要执行的各种statement（statement、preparedStatemnt、CallableStatement）配置起来，并通过java对象和statement中的sql进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射成java对象并返回。



一. MyBatis的框架核心

1、 mybatis配置文件，包括**Mybatis全局配置文件和Mybatis映射文件**，其中 全局配置文件配置了数据源、事务等信息；  映射文件配置了SQL执行相关的信息。

2、 mybatis通过读取配置文件信息（全局配置文件和映射文件），构造出**SqlSessionFactory**，即会话工厂。

3、 通过SqlSessionFactory，可以创建**SqlSession**即会话。Mybatis是通过SqlSession来操作数据库的。

4、 SqlSession本身不能直接操作数据库，它是通过底层的**Executor**执行器接口来操作数据库的。Executor接口有两个实现类，一个是普通执行器，一个是**缓存执行器（默认）**。

5、 Executor执行器要处理的SQL信息是封装到一个底层对象**MappedStatement**中。该对象包括：SQL语句、输入参数映射信息、输出结果集映射信息。其中输入参数和输出结果的映射类型包括**HashMap**、集合对象、**POJO对象类型**。



二、添加log4j.properties

Mybatis使用的日志包是log4j的，所以需要添加log4j.properties。

在classpath下创建log4j.properties如下：【文件内容可以从mybatis-3.2.7.pdf中拷贝】

```properties
# Global logging configuration
log4j.rootLogger=DEBUG, stdout

# Console output...
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] - %m%n
```

日志级别在开发阶段设置成DEBUG，在生产阶段设置成INFO或者ERROR。





三、开发步骤

```
1、	创建PO（model）类，根据需求创建；
2、	创建全局配置文件SqlMapConfig.xml；
3、	编写映射文件；
4、	加载映射文件，在SqlMapConfig.xml中进行加载；
5、	编写测试程序，即编写Java代码，连接并操作数据库。

思路：
a)	读取配置文件；
b)	通过SqlSessionFactoryBuilder创建SqlSessionFactory会话工厂。
c)	通过SqlSessionFactory创建SqlSession。
d)	调用SqlSession的操作数据库方法。
e)	关闭SqlSession。

```





#### 1.全局配置文件



```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <!-- 1.配置数据库链接 -->
  <properties resource="db.properties"/>
  
  
  <!-- 2.配置别名 -->
  <typeAliases>
    <typeAlias type="cn.coder.model.User" alias="_user"/>
    <!--指定包名 别名就是类名 第一个大写字母改成小写-->
    <package name="cn.coder.model"/>
  </typeAliases>
  
  
  
  <!-- 3.配置mybatis的环境信息 -->
  <environments default="development">
    <environment id="development">
      <!-- 配置JDBC事务控制，由mybatis进行管理 -->
      <transactionManager type="JDBC"/>
      <!-- 配置数据源，采用dbcp连接池 -->
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>

  
  
  <!-- 4.告诉mybatis加载映射文件 -->
  <mappers>
    <mapper resource="cn/coder/sqlmap/User.xml"/>
  </mappers>
  
  
  
</configuration>
```





#### 2.映射文件

在classpath下，创建sqlmap文件夹。在sqlmap目录下，创建User.xml映射文件。

cn/coder/sqlmap/User.xml   映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--
 namespace：命名空间，它的作用就是对SQL进行分类化管理，可以理解为SQL隔离
 注意：使用mapper代理开发时，namespace有特殊且重要的作用
 -->
<mapper namespace="user">
  <!--
        [id]：statement的id，要求在命名空间内唯一
        [parameterType]：入参的java类型
        [resultType]：查询出的单条结果集对应的java类型
        [#{}]： 表示一个占位符?
        [#{id}]：表示该占位符待接收参数的名称为id。注意：如果参数为简单类型时，#{}里面的参数名称可以是任意定义
     -->
  <select id="findUserById" parameterType="int" resultType="cn.coder.model.User">
    SELECT * FROM USER WHERE id = #{id}
  </select>
</mapper>

```



#### 3.database链接配置   db.properties

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useUnicode=true&characterEncoding=utf8
username=root
password=root
```



1. 增加记录

```xml
<!--插入-->
<insert id="insertUser" parameterType="cn.coder.model.User">
  
  <!--
		-- 插入时自动返回主键id --
   [selectKey标签]：通过select查询来生成主键
   [keyProperty]：指定存放生成主键的属性
   [resultType]：生成主键所对应的Java类型
   [order]：指定该查询主键SQL语句的执行顺序，相对于insert语句
   [last_insert_id]：MySQL的函数，要配合insert语句一起使用 
	-->
  <selectKey keyProperty="id" resultType="int" order="AFTER">
    select last_insert_id()
  </selectKey>
  <!-- 如果主键的值是通过MySQL自增机制生成的，那么我们此处不需要再显示的给ID赋值 -->
  insert into user (username, sex, birthday, address) values (#{username},#{sex},#{birthday},#{address})
</insert>
```

2. 删除记录

```xml
<!--删除-->
<delete id="deleteUser" parameterType="int">
  delete from user where id = #{id}
</delete>
```

3. 模糊查询和直接查询

```xml
<!--
   [id]：statement的id，要求在命名空间内唯一
   [parameterType]：入参的java类型
   [resultType]：查询出的单条结果集对应的java类型
   [#{}]： 表示一个占位符?
   [#{id}]：表示该占位符待接收参数的名称为id。注意：如果参数为简单类型时，#{}里面的参数名称可以是任意定义
-->
<select id="findUserById" parameterType="int" resultType="cn.coder.model.User">
  SELECT * FROM USER WHERE id = #{id}
</select>


<!--
  [${}]：表示拼接SQL字符串
   [${value}]：表示要拼接的是简单类型参数。
   注意：
  1、如果参数为简单类型时，${}里面的参数名称必须为value
  2、${}会引起SQL注入，一般情况下不推荐使用。但是有些场景必须使用${}，比如order by ${colname}
 -->
<select id="findUserByName" parameterType="String" resultType="cn.coder.model.User">
  SELECT * FROM USER WHERE username like '%${value}%'
</select>
<!-- select出来的记录  会自动封装成User对象 -->
```

4. 更新记录

```xml
<!--更新-->
<update id="updateUser" parameterType="cn.coder.model.User">
  update user set username=#{username}, address = #{address}, sex=#{sex} where id = #{id}
</update>
```









#### 单元测试调用：



```java
SqlSession sqlSession = null;

@Before
public void before() throws IOException {
  // 读取配置文件   SqlMapConfig.xml   注意是org.apache.ibatis.io.Resources
  InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
  // 创建SqlSessionFactory会话工厂
  SqlSessionFactory build = new SqlSessionFactoryBuilder().build(is);
  // 通过SqlSessionFactory创建SqlSession会话
  sqlSession = build.openSession();
  // 调用sqlSession的操作数据库的方法  第一个参数为mapper映射的id  第二个是参数
  System.out.println("准备");
}

@After
public void after() {
  // 关闭sqlSession
  System.out.println("提交");
  sqlSession.close();
}

@Test
public void test01() throws IOException {
 	// 此处进行CURD操作
  sqlSession.commit();
}
```





关于返回主键

```
ORCLE主键    SELECT user_seq.nextval() FROM dual
主键返回之MySQL自增UUID  SELECT UUID()
主键返回之MySQL自增主键   SELECT LAST_INSERT_ID()
```









#### 总结：

```
parameterType和resultType
	parameterType指定输入参数的java类型，可以填写别名或Java类的全限定名。
	resultType指定输出结果的java类型，可以填写别名或Java类的全限定名。

#{}和${}


#{}：相当于预处理中的占位符？。
#{} 里面的参数表示接收java输入参数的名称。
#{} 可以接受HashMap、POJO类型的参数。
当接受简单类型的参数时，#{}里面可以是value，也可以是其他。
#{} 可以防止SQL注入。

${}：相当于拼接SQL串，对传入的值不做任何解释的原样输出。
${} 会引起SQL注入，所以要谨慎使用。
${} 可以接受HashMap、POJO类型的参数。
当接受简单类型的参数时，${}里面只能是value。

selectOne和selectList
  selectOne：只能查询0或1条记录，大于1条记录的话，会报错：
  selectList：可以查询0或N条记录

```

