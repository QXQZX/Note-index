```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

  <bean id="stu" class="cn.coder.spring.Student">
    <property name="name" value="张国辉"/>
    <property name="age" value="18"/>
    <property name="gender" value="男"/>
    
    <!--封装list集合-->
    <property name="cars">
      <list>
        <value>ofo</value>
        <value>mobai</value>
        <value>玛莎</value>
      </list>
    </property>
    
    <!--封装Set-->
    <property name="pats">
      <set>
        <value>小黑</value>
        <value>小黄</value>
        <value>小蓝</value>
      </set>
      
    </property>
    
    <!--封装map-->
    <property name="infos">
      <map>
        <entry key="name" value="zhj"/>
        <entry key="age" value="19"/>
        <entry key="gender" value="男"/>
      </map>
    </property>

    <!--封装properties-->
    <property name="mysqlinfos">
      <props>
        <prop key="url">mysql:jdbc://localhost:3307/db</prop>
        <prop key="root">admin</prop>
        <prop key="pwd">root</prop>
      </props>
    </property>
    
    <!--封装数组-->
    <property name="family">
      <array>
        <value>哥哥</value>
        <value>姐姐</value>
        <value>弟弟</value>
      </array>
    </property>
  </bean>
</beans>
```

