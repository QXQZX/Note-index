Beans.xml

```xml
<!--    读取db.properties数据-->
<context:property-placeholder location="classpath:db.properties"/>
<!--    配置数据库链接-->
<bean id="dataSource" class="">
  <property name="driverClass" value=""/>
  <property name="jdbcUrl" value=""/>
  <property name="user" value=""/>
  <property name="password" value=""/>
</bean>
```

