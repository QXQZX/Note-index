## AOP

一.概述  AOP面向切面编程



1)      在软件业，**AOP**为 **Aspect Oriented Programming**的缩写，意为：**面向切面编程**，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。

2)      AOP是OOP（面向对象编程）的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。

3)      利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

4)      AOP采取横向抽取机制，取代了传统纵向继承体系重复性代码

**5)**      **经典应用：事务管理、性能监视、安全检查、缓存** **、日志等**【画图】

6)      Spring AOP使用纯Java实现，不需要专门的编译过程和类加载器，在运行期通过代理方式向目标类织入增强代码

7)      **AspectJ**是一个基于Java语言的AOP框架，Spring2.0开始，Spring AOP引入对Aspect的支持，AspectJ扩展了Java语言，提供了一个专门的编译器，在编译时提供横向代码的织入





二.实现原理

a.   aop底层采用代理机制 进行实现

b.   接口 + 实现类 ： spring采用jdk的动态代理Proxy

c.   实现类：  spring 采用 cglib 字节码增强



三、AOP术语

1) **target**：目标类，需要被代理的类。例如：UserService

2) **Joinpoint**(连接点):所谓连接点是指那些可能被拦截到的方法。例如：所有的方法

3) **PointCut** 切入点：已经被增强的连接点。例如：addUser()

4) **advice** **通知增强**，**增强代码**。例如：after、before

5)   **Weaving**(织入):是指把增强advice应用到目标对象target来创建新的代理对象proxy的过程.

6) **proxy** 代理类

7)  **Aspect**(切面): 是切入点pointcut和通知advice的结合

​       一个线是一个特殊的面。

​       一个切入点和一个通知，组成成一个特殊的面。

![aop.png](https://tuku.jdblog.cn/2019/07/01/aop.png)



--------------



#### 手动代理

略。。。



#### JDK自动代理

略。。。



#### Cglib   ||    AOP联盟

略。。。





#### Spring编写代理半自动

1.定义切面类  实现aopalliance包下的MethodIntercepto接口

```java
public class MyAspect implements MethodInterceptor {
    @Override
    public Object invoke(MethodInvocation methodInvocation) throws Throwable {
        // 拦截方法
        System.out.println("开启事务");
        // 放行
        Object proceed = methodInvocation.proceed();
        System.out.println("拦截。。。");

        System.out.println("提交事务。。。");

        return null;
    }
}

```

2.serviceImpl类实现 service的接口

3.配置beans.xml

```xml
<!--    spring编写代理半自动-->

<!-- 业务类 -->
<bean id="stuService" class="cn.coder.aspect.stuServiceImpl"/>
<!-- 切面类 -->
<bean id="myAspect" class="cn.coder.aspect.MyAspect"/>


<!-- 配置代理对象 
		使用工厂bean创建代理
		interfaces：确定接口  多接口使用array 单个使用value
		target：目标      
		interceptorNames：通知，切面类
-->
<bean id="serviceProxy" class="org.springframework.aop.framework.ProxyFactoryBean">
  <property name="interfaces" value="cn.coder.aspect.stuService"/>
  <property name="target" ref="stuService"/>
  <property name="interceptorNames" value="myAspect"/>
</bean>
```

4.测试调用

```java
@Test
public void test3() {
  ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
  stuService proxy = (stuService) context.getBean("serviceProxy");

  proxy.before();

}
```





#### Spring编写代理全自动

要明白什么是全自动织入

1.导入需要的jar包 				aspectjweaver-1.8.4.jar

2.spring的AOP配置

beans.xml  添加内容

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/aop
                           http://www.springframework.org/schema/aop/spring-aop.xsd">
  <!--    spring编写代理全自动-->

  <!-- 业务类 -->
  <bean id="stuService" class="cn.coder.aspect.stuServiceImpl"/>
  <!-- 配置切面对象 -->
  <bean id="myAspect" class="cn.coder.aspect.MyAspect"/>

  <!--    配置aop
        1.导入命令空间 上面的aop空间
        2.proxy-target-class="true" 使用cglib代理
        3.aop:pointcut  切入点，从目标对象获取具体方法
            切入点表达式 expression="execution(* cn.coder.aspect.*.*(..))"
        4.特殊的切面    advice-ref 通知    pointcut-ref 切入点引用
-->
  <aop:config proxy-target-class="true">
    <aop:aspect ref="myAspect">
      <aop:pointcut id="myPointcut" expression="execution(* cn.coder.aspect.*.*(..))"/>
      <aop:before method="before" pointcut-ref="myPointcut"/>
      <aop:after-returning method="after" pointcut-ref="myPointcut"/>
    </aop:aspect>
  </aop:config>
</beans>
```

测试

```java
//全自动
@Test
public void test4() {
  ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
  stuService proxy = (stuService) context.getBean("stuService");
  proxy.before();
}
```





