#### beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop
                           http://www.springframework.org/schema/aop/spring-aop.xsd
                           http://www.springframework.org/schema/tx
                           http://www.springframework.org/schema/tx/spring-tx.xsd">

  <!--spring编写代理全自动-->
  <!--扫描注解-->
  <context:component-scan base-package="cn.coder"/>
  <!--确定aop注解生效-->
  <aop:aspectj-autoproxy/>


</beans>
```



#### 接口实现类添加注解

@Service("xxx")   

```java
package cn.coder.aspect;

import org.springframework.stereotype.Service;

@Service()
public class stuServiceImpl implements stuService {
    @Override
    public int add() {
        System.out.println("add。。。");
        return 1;
    }

    @Override
    public int delete() {
        System.out.println("del。。。");
//        int i = 10 / 0;
        return 1;
    }
}

```





#### 切面类添加注解

@Component   @Aspect

````java
package cn.coder.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

/**
 * 切面对象
 */
@Component
@Aspect
public class MyAspect {
    // 手动添加切入点
    @Pointcut("execution(* cn.coder.aspect.stuServiceImpl.*(..))")
    public void myPoint() {
    }

    @Before(value = "myPoint()")
    public void before() {
        System.out.println("前。。。。");
    }

    @AfterReturning(value = "myPoint()", returning = "retvalue")
    public void afterRet(JoinPoint jp, Object retvalue) {
        System.out.println(jp.toString()); // JoinPoint切入点
        System.out.println("返回值" + retvalue);
        System.out.println("后。。。。");
    }

    @Around(value = "myPoint()")
    public Object around(ProceedingJoinPoint pjp) throws Throwable {

        System.out.println("前环绕" + pjp.getSignature().getName());
        Object retObj = pjp.proceed();
        System.out.println("后环绕" + pjp.getSignature().getName());
        return retObj;
    }


    @AfterThrowing(value = "myPoint()", throwing = "e")
    public void myAfterThrowing(JoinPoint jp, Throwable e) {
        System.out.println("异常通知。。。" + jp.getSignature().getName() + "===" + e.getMessage());
    }

    @After("myPoint()")
    public void after() {
        System.out.println("最后通知。。");
    }
}

````





#### 测试类

```java
@Test
public void test5() {
  ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
  stuService proxy = context.getBean(stuService.class);
  proxy.delete();
}
```



### 注解总结

@Aspect  声明切面，修饰切面类，从而获得 通知。

通知

​       @Before 前置

​       @AfterReturning 后置

​       @Around 环绕

​       @AfterThrowing 抛出异常

​       @After 最终

切入点

​       @PointCut ，修饰方法 private void xxx(){}  之后通过“方法名”获得切入点引用

