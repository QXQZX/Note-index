导包：

aopalliance-1.0.jar     AOP联盟规范

aspectjweaver-1.8.4.jar   规范

spring-aop-4.3.18.RELEASE.jar   AOP实现

spring-aspects-4.3.18.RELEASE.jar    aspectj实现

 

Beans.xml配置

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

  <!-- 业务类 -->
  <bean id="userService" class="..."/>
  <!-- 切面类 -->
  <bean id="myAspect" class="cn.coder.aspect"/>

  <aop:config>
    <aop:aspect>
      <!-- 配置切点 -->
      <aop:pointcut id="myPointcut" expression="execution(* .......)"/>
      <!-- 前置通知 -->
      <aop:before method="before" pointcut-ref="myPointcut"/>
      <!-- 环绕通知 -->
      <aop:around method="around" pointcut-ref="myPointcut"/>
      <!-- 后置通知 returning="retValue"是第二个参数 -->
      <aop:after-returning method="afterRet" pointcut-ref="myPointcut" returning="retValue"/>
      <!-- 异常抛出通知 throwing="e"是第二个参数 -->
      <aop:after-throwing method="..." pointcut-ref="myPointcut" throwing="e"/>
      <!-- 最终通知 -->
      <aop:after method="after" pointcut-ref="myPointcut"/>
    </aop:aspect>
  </aop:config>
</beans>
```



切面类：

```java
package cn.coder.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;

/**
 * 切面对象
 */
public class MyAspect {
  
    public void before(JoinPoint jp) {
        System.out.println("前置通知");
    }

    public void afterRet(JoinPoint jp, Object retvalue) {
        System.out.println(jp.toString()); // JoinPoint切入点
        System.out.println("返回值" + retvalue);
        System.out.println("后置通知");
    }

    public Object around(ProceedingJoinPoint pjp) throws Throwable {

        System.out.println("前环绕" + pjp.getSignature().getName());
        Object retObj = pjp.proceed();
        System.out.println("后环绕" + pjp.getSignature().getName());
        return retObj;
    }

    public void myAfterThrowing(JoinPoint jp, Throwable e) {
        System.out.println("异常通知" + jp.getSignature().getName() + "===" + e.getMessage());
    }

    public void after() {
        System.out.println("最后通知");
    }
}

```

