### 【了解】



第一种  BeanNameUrlHandlerMapping

通过 访问url的名字  找到对应的bean的name的控制器

````xml
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>

<bean name="/user.do" class="cn.coder.admin.web.controller.UserController"/>
````



第二种  SimpleUrlHandlerMapping

通过 key找到bean的id控制器

````xml
<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
  <property name="mappings">
    <props>
      <prop key="/user1.do">userController</prop>
      <prop key="/user2.do">userController</prop>
      <prop key="/user3.do">userController</prop>
    </props>
  </property>
</bean>

<bean id="userController" class="cn.coder.admin.web.controller.UserController"/>
````



第三种  ControllerClassNameHandlerMapping

不用配置访问路径   默认的访问路径就是 控制器名字首字母小写  加.do     userController.do

````xml
<bean class="org.springframework.web.servlet.mvc.support.ControllerClassNameHandlerMapping"/>
````

