不在需要dao操作的映射文件  而是在注解中写sql语句

#### 全局配置文件

```xml
<!--    告诉mybatis加载映射文件  
	不在需要mapper  
-->
<mappers>
  <!--mapper resource="cn/coder/mapper/UserMapper.xml"/-->
  <mapper class="cn.coder.mapper.UserMapper"/> <!--UserMapper是接口-->
</mappers>
```



#### 下面代码实例：

只有 UserDao.java   接口

```java
package cn.coder.mapper;

import cn.coder.model.User;

/**
 * 映射的dao接口
 */
public interface UserMapper {
  // 查找用户 返回值为 mysql生成的自增id
  @Insert("insert into user (username, sex, birthday, address) values (#{username},#{sex},#{birthday},#{address})")
  public int save(User user);

  @Select("SELECT * FROM USER WHERE id = #{id}")
  public User findUserById(int id);
}

```

