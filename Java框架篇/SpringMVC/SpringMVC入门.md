### SpringMVC 入门

MVC

M:Model

V:View

C:Controller - servlet/action/controller

 

Spring MVC是Spring提供的一个强大而灵活的web框架。借助于注解，Spring MVC提供了几乎是POJO的开发模式，使得控制器的开发和测试更加简单。这些控制器一般不直接处理请求，而是将其委托给Spring上下文中的其他bean，通过Spring的依赖注入功能，这些bean被注入到控制器中。

 

Spring MVC主要由DispatcherServlet、处理器映射【找控制器】、适配器【调用控制器的方法】、控制器【业务】、视图解析器、视图组成。





第一步：导包：

略


第二步：在webxml中配置DispatcherServlet

```xml
<!-- 把所有的请求转发给Spring去管理 -->
<servlet>
  <servlet-name>DispatcherServlet</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
  <servlet-name>DispatcherServlet</servlet-name>
  <url-pattern>*.do</url-pattern>
</servlet-mapping>

<!-- 配置编码过滤器  -->
<filter>
  <filter-name>EncodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
</filter>

<filter-mapping>
  <filter-name>EncodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>

```

第三步：在WEB-INF目录下创建DispatcherServlet-servlet.xml  并添加如下配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:aop="http://www.springframework.org/schema/aop" xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans 
		http://www.springframework.org/schema/beans/spring-beans-3.2.xsd 
		http://www.springframework.org/schema/mvc 
		http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd 
		http://www.springframework.org/schema/context 
		http://www.springframework.org/schema/context/spring-context-3.2.xsd 
		http://www.springframework.org/schema/aop 
		http://www.springframework.org/schema/aop/spring-aop-3.2.xsd 
		http://www.springframework.org/schema/tx 
		http://www.springframework.org/schema/tx/spring-tx-3.2.xsd">
		
  
  <!-- 1. 配置url处理器映射，springmvc默认的处理器映射器
			 BeanNameUrlHandlerMapping:根据bean的name属性的url去找handlerController -->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
    <!-- 2. 配置控制器处理适配器 执行Controller 处理映射-->
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
  
 <!-- <bean class="org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter"/>-->
    <!-- 3.配置一个控制器 相当于赔了一个访问路径-->
    <bean name="/user.do" class="com.gyf.backoffice.web.controller.UserController"/>
    <!-- 4.配置springmvc视图解析器
        视图解析器解析的视频路径为：前缀 + 后缀 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views"/>
        <property name="suffix" value=".jsp"/>
    </bean>
  
</beans>

```

