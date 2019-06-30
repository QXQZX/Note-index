## MyBatis的Dao编写

### 旧的实现方式：一般不用，有更多好方式



一个UserDao接口，一个UserDaoImpl的实现类

实现类中添加一个私有的SqlSessionFactory。  利用工厂获取SqlSession会话   与  映射文件、 全局配置文件完成dao操作



### 新的实现方式【mapper代理方式实现】



Mapper代理的开发方式，程序员只需要编写mapper接口（相当于dao接口）即可。Mybatis会自动的为mapper接口生成**动态代理实现类**。(jdk自带的proxy代理)

**不过要实现mapper代理的开发方式，需要遵循一些开发规范**



#### 开发规范

```
1.	mapper接口的全限定名要和mapper映射文件的namespace的值相同。
2.	mapper接口的方法名称要和mapper映射文件中的statement的id相同；
3.	mapper接口的方法参数只能有一个，且类型要和mapper映射文件中statement的parameterType的值保持一致。
4.	mapper接口的返回值类型要和mapper映射文件中statement的resultType值或resultMap中的type值保持一致；

通过规范式的开发mapper接口，可以解决原始dao开发当中存在的问题：
*	模板代码已经去掉；
*	剩下去不掉的操作数据库的代码，其实就是一行代码。这行代码中硬编码的部分，通过第一和第二个规范就可以解决。

```



#### 下面代码实例：

UserDao.java   接口

```java
package cn.coder.mapper;

import cn.coder.model.User;

/**
 * 映射的dao接口
 */
public interface UserMapper {
		// 查找用户 返回值为 mysql生成的自增id
    public int save(User user);

    public User findUserById(int id);
}

```

UserMapper.xml文件  

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace: 命名空间与接口的全名相对应-->
<mapper namespace="cn.coder.mapper.UserMapper">
  	<!--id与方法名称想对应 parameterType与传入的参数类型相对应 resultType与返回值类型相对-->
    <insert id="save" parameterType="cn.coder.model.User">
        <selectKey keyProperty="id" resultType="int" order="AFTER">
            select last_insert_id()
        </selectKey>
        insert into user (username, sex, birthday, address) values (#{username},#{sex},#{birthday},#{address})
    </insert>
  
    <select id="findUserById" parameterType="int" resultType="cn.coder.model.User">
        SELECT * FROM USER WHERE id = #{id}
    </select>
</mapper>
```

在全局配置文件中添加映射 SqlMapConfig.xml

```xml
<!--    告诉mybatis加载映射文件    -->
<mappers>
  <!--配置 配置文件-->
  <mapper resource="cn/coder/mapper/UserMapper.xml"/>
  <!--配合注解 世界声明接口类-->
  <mapper class="cn.coder.mapper.UserMapper"/>
  <!--直接配置包【推荐】-->
  <package name="cn.coder.mapper"/>
</mappers>
```



#### 单元测试

```java
SqlSession sqlSession = null; // 全局SqlSession对象声明

@Before
public void before() throws IOException {
  System.out.println("before.....获取sqlsession");
  
  // 加载全局配置文件
  InputStream is = Resources.getResourceAsStream("SqlMapConfig.xml");
	// 创建SqlSession工厂
  SqlSessionFactory ssf = new SqlSessionFactoryBuilder().build(is);
  // 获取SqlSession对话
  sqlSession = ssf.openSession();
}
@After
public void after() {
  System.out.println("after..... 关闭sqlsession");
  sqlSession.close();
}

@Test
public void test01() {
  UserMapper mapper = sqlSession.getMapper(UserMapper.class);
  
  // 查找用户
  User user = mapper.findUserById(1);
  System.out.println(user);

  // 添加用户
  User u = new User("xxxx", "x", new Date(), "xx");
  mapper.save(u);
  sqlSession.commit();
}
```



