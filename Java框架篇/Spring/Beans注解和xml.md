

#### 配置一个bean对象的三种方式

```xml
<!--    配置一个bean对象
    bean的作用域
    scope=singleton: 单例   默认
    scope=prototype: 多例   多个对象  每次都new一个新的
-->

<!--    第一种方式-->
<bean id="UserService1" class="cn.coder.spring.UserServiceImpl" scope="singleton">
  <!--    依赖注入数据 会调用set  get属性-->
  <property name="name" value="张国辉"/>
</bean>


<!--    第二种方式-->
<bean id="UserService2" class="cn.coder.spring.UserServiceFactory1" factory-method="creatUserService">
  <property name="name" value="zgh"/>
</bean>


<!--    第三种方式-->
<bean id="factory2" class="cn.coder.spring.UserServiceFactory2"/>
<bean id="UserService3" factory-bean="factory2" factory-method="creatUserService">
  <property name="name" value="哈哈哈哈"/>
</bean>

```

参数注入-构造方法

```xml
<!--第一种-->
<bean id="stu" class="cn.coder.spring.Student">
  <constructor-arg name="name" value="张国辉"/>
  <constructor-arg name="age" value="18"/>
</bean>
<!--第二种-->
<bean id="stu" class="cn.coder.spring.Student">
  <constructor-arg index="0" value="张国辉" type="java.lang.String"/>
  <constructor-arg index="1" value="男" type="java.lang.String"/>
  <constructor-arg index="2" value="18" type="int"/>
</bean>

```

参数注入-setter方法

```xml
<bean id="stu" class="cn.coder.spring.Student">
  <property name="name" value="张国辉"/>
  <property name="age" value="18"/>
  <property name="gender" value="男"/>
</bean>
```

参数注入-p命名空间方法(了解)

```xml
添加
xmlns:p="http://www.springframework.org/schema/p"

<bean id="" class="" p:xxx="xxx" p:xxxx="xxxx" />
```





#### 注解配置bean对象

1. 添加xmlns  (context相关的)

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
 							             http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd">
  
  
    <!--    开启注解-->
    <context:annotation-config/>
    <!--    注解的位置  所有在cn.coder.spring包下的类都会进行扫描-->
    <context:component-scan base-package="cn.coder.spring"/>
</beans>
```

2. 在类中添加注解  @Component   ||  @Component("id")
3. 有无id的  获取方式

```java
// 无id  
// 如果@Component  没有配置id  则通过  类名.class（或者是 接口名.class）获取
UserServiceImpl bean = (UserServiceImpl) context.getBean(UserService.class); // 接口
UserServiceImpl bean = context.getBean(UserServiceImpl.class);//类名

// 有id
// 如果@Component("userService")   则通过id获取
UserServiceImpl bean = (UserServiceImpl) context.getBean("userService");
```



类的注解：

```java
@Component("id")

@Repository("") // dao层
@Controller("")  // web层
@Service("myUserService") // service 层  

@Autowired // spring自动注入属性  若是接口则自动寻找接口实现类  若是类自动寻找类
@Qualifier("myUserService")  // 根据指定的id注入属性

@Resource(name = "xxx")
@Scope("prototype") // 多例  默认单例
@PostConstruct // 自定义初始化方法
@PreDestroy // 自定义销毁方法
```

其中

```java
@Resource(name = "myUserService")  // 等价于下面两行  [用的少]

@Autowired // spring自动注入属性  [用的多]
@Qualifier("myUserService")  // 根据指定的id注入属性 [用的少]
```







关闭容器

```java
context.getClass().getMethod("close").invoke(context); // 反射 思想
```



