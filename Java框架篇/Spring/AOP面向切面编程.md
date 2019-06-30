### AOP

1.概述  AOP面向切面编程

2.实现原理

a.   aop底层采用代理机制 进行实现

b.   接口 + 实现类 ： spring采用jdk的动态代理Proxy

c.   实现类：  spring 采用 cglib 字节码增强









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
<bean id="stuService" class="cn.coder.aspect.stuServiceImpl"/>
<bean id="myAspect" class="cn.coder.aspect.MyAspect"/>
<!--    配置代理对象-->
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

