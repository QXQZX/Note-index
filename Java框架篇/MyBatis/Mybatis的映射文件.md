

### 输入映射ParameterType

指定输入参数的java类型，可以使用别名或者类的全限定名。它可以接收**简单类型**,POJO**对象、HashMap**。

 

传递简单类型



传递POJO包装对象

开发中通过pojo传递查询条件 ，查询条件是综合的查询条件，不仅包括用户查询条件还包括其它的查询条件（比如将用户购买商品信息也作为查询条件），这时可以使用包装对象传递输入参数。

**需求**

综合查询用户信息，需要传入查询条件复杂，比如（用户信息、订单信息、商品信息）。

vo:键值对对象，相对于kv

po:persist object 持久化对象

pojo:简单的java对象

entity:实体

 

#### 定义POJO包装类

```java
package cn.coder.model;

public class UserQueryVO {
    private User user;

    public User getUser() {
        return user;
    }

    public void setUser(User user) {
        this.user = user;
    }
}

```



#### 修改UserMapper.java

```java
import java.util.List;
import java.util.Map;

/**
 * 映射的dao接口
 */
public interface UserMapper {
    public int findUserByVO(UserQueryVO vo);

}
```



#### 修改UsrMappler.xml

```xml
<!--查询用户个数  返回数据的基本类型-->
<select id="findUserByVO" parameterType="cn.coder.model.UserQueryVO" resultType="int">
  select count(*) from user where sex = #{user.sex}
</select>
```



#### 测试

```java
/*UserQueryVO 测试*/
@Test
public void test03() {
  UserMapper mapper = sqlSession.getMapper(UserMapper.class);
  UserQueryVO vo = new UserQueryVO();
  User user = new User();
  user.setSex("1");
  vo.setUser(user);
  int i = mapper.findUserByVO(vo);

  System.out.println(i);
}

```









## 输出映射 resultType/resultMap

### resultType

使用resultType进行结果映射时，查询的列名和映射的pojo属性名完全一致，该列才能映射成功。

如果查询的列名和映射的pojo属性名全部不一致，则不会创建pojo对象；

如果查询的列名和映射的pojo属性名有一个一致，就会创建pojo对象。

**总结：**

输出单个pojo对象和pojo列表时，mapper映射文件中的resultType的类型是一样的，mapper接口的方法返回值不同。

同样的mapper映射文件，返回单个对象和对象列表时，mapper接口在生成动态代理的时候，会根据返回值的类型，决定调用selectOne方法还是selectList方法。

待补充。。。。



### resultMap

如果查询出来的列名和属性名不一致，通过定义一个**resultMap**将列名和POJO**属性名**之间作一个映射关系。

1、 定义resultMap

```xml
<!--设置返回数据为  resultMap-->
<resultMap id="userResultMap" type="user">
  <id property="id" column="id_"/>
  <result property="username" column="username_"/>
  <result property="sex" column="sex_"/>
  <result property="birthday" column="birthday_"/>
  <result property="address" column="address_"/>
</resultMap>
```



2、使用resultMap作为statement的输出映射类型

```xml
<select id="findUsersByIdResMap" parameterType="int" resultMap="userResultMap">
  select
  id id_,
  username username_,
  sex sex_,
  birthday birthday_,
  address address_
  from user where id=#{id}
</select>
```



3、修改UserMapper.java

```java
public User findUsersByIdResMap(int id);
```



4、测试

```java
/*ResultMap  测试*/
@Test
public void test04() {
  UserMapper mapper = sqlSession.getMapper(UserMapper.class);
  User user = mapper.findUsersByIdResMap(1);
  System.out.println(user);
}
```

