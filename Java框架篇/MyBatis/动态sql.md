

### 1.if和where

If标签：

​	作为判断入参来使用的，如果符合条件，则把if标签体内的SQL拼接上。

​	**注意：用if进行判断是否为空时，不仅要判断null，也要判断空字符串 ' ' **

Where标签：  会去掉条件中的第一个符号  ( and   or )

```xml
<!-- 6. 动态sql  where if 条件使用 -->
<select id="findUserList" parameterType="userQueryVO" resultType="user">
  select * from users
  <where>
    <if test="user != null">
      <if test="user.sex != null and user.sex != ''">sex=#{user.sex}</if>
      <if test="user.username != null and user.sex != ''">and username like '%${user.username}%'</if>
    </if>
  </where>
</select>
```




### 2.sql 片段

```xml
<sql id="test">
  <if test="user != null">
    <if test="user.sex != null and user.sex != ''">sex=#{user.sex}</if>
    <if test="user.username != null and user.sex != ''">and username like '%${user.username}%'</if>
  </if>
</sql>

<select id="findUserList" parameterType="userQueryVO" resultType="user">
  select * from users
  <where>
    <include refid="test"/>
  </where>
</select>

```



### 3.forEach

```xml
<!-- 7. foreach 遍历 -->
<select id="findUsersUseForeach" parameterType="userQueryVO" resultType="user">
  select * from users
  <where>
    <if test="ids != null and ids.size > 0" >
      <!--
                    collection :   集合  写vo里面的集合
                    items： 集合元素接收变量
                    open:  开始遍历拼接时候的字符串
                    close：  结束遍历拼接时候的字符串
                    separator ： 便利出每个元素后的分割符
                -->
      <foreach collection="ids" item="id" open="id in(" close=")" separator=",">
        #{id}
      </foreach>
    </if>
  </where>
</select>

<!-- 7. foreach 遍历  传入list方式  名字固定写list-->
<select id="findUsersUseForeach" parameterType="list" resultType="user">
  select * from users
  <where>
    <if test="list != null and list.size > 0" >
      <!--
                    collection :   集合  写vo里面的集合
                    items： 集合元素接收变量
                    open:  开始遍历拼接时候的字符串
                    close：  结束遍历拼接时候的字符串
                    separator ： 便利出每个元素后的分割符
                -->
      <foreach collection="list" item="id" open="id in(" close=")" separator=", ">
        #{id}
      </foreach>
    </if>
  </where>
</select>
```

