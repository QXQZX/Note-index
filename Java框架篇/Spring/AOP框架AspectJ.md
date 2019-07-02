##  AspectJ

一、AspectJ简介

* AspectJ是一个基于Java语言的AOP框架

* Spring2.0以后新增了对AspectJ切点表达式支持

* @AspectJ 是AspectJ1.5新增功能，通过JDK5注解技术，允许直接在Bean类中定义切面

* **新版本Spring框架，建议使用AspectJ方式来开发AOP**

* **主要用途：自定义开发**

 

二、切入点表达式【掌握】

### execution()  

用于描述方法 【掌握】



 

**修饰符，一般省略**

​       public    公共方法                  *    任意

**返回值，不能省略**

​       void               返回没有值

​       String             返回值字符串

​       \*                  任意

**包，[省略]**

​       com.gyf.crm                  固定包

​       com.gyf.crm.*.service    crm包下面子包任意 （例如：com.gyf.crm.staff.service）

​       com.gyf.crm..                crm包下面的所有子包（含自己）

​       com.gyf.crm.*.service..  crm包下面任意子包，固定目录service，service目录任意包

**类，[省略]**

​       UserServiceImpl                   指定类

​       *Impl                                  以Impl结尾

​       User*                                  以User开头

​       \*                                        任意

**方法名，不能省略**

​       addUser                              固定方法

​       add*                                          以add开头

​       *Do                                    以Do结尾

​       \*                                        任意

**(参数)**

​       ()                                        无参

​       (int)                                    一个整型

​       (int ,int)                               两个

​       (..)                                      参数任意

**throws  可省略，一般不写**。

 

案例1：  **execution(\* com.gyf.crm.\*.service..\*.\*(..))**

案例2：

```xml
<aop:pointcut id="myPointCut" expression="execution(* com.gyf.crm.service.*.*(..)) || execution(* com.gyf.*Do.*(..))" />
```

within:

匹配包或子包中的方法(了解)             within(com.gyf.aop..*)   

 this:

匹配实现接口的代理对象中的方法(了解)



 target:

匹配实现接口的目标对象中的方法(了解)



args:

匹配参数格式符合标准的方法(了解)



bean(id)  

对指定的bean所有的方法(了解)



 

 

三、AspectJ 通知类型

aop联盟定义通知类型，具有特性接口，必须实现，从而确定方法名称。
aspectj 通知类型，只定义类型名称，以及方法格式。
个数：6种，**知道5种，掌握1种**。

```
before:前置通知 (应用：各种校验)
			 在方法执行前执行，如果通知抛出异常，阻止方法运行
			 
afterReturning:后置通知(应用：常规数据处理)
			 方法正常返回后执行，如果方法中抛出异常，通知无法执行
			 必须在方法执行后才执行，所以可以获得方法的返回值。
			 
around:环绕通知(应用：十分强大，可以做任何事情)
			 方法执行前后分别执行，可以阻止方法的执行
			 
**必须手动执行目标方法**
afterThrowing:抛出异常通知(应用：包装异常信息) 
			 方法抛出异常后执行，如果方法没有抛出异常，无法执行
after:最终通知(应用：清理现场)
			 方法执行完毕后执行，无论方法中是否出现异常 
```





