### servlet：  server  applet

概念：  运行在服务期短的小程序

servlet是一个接口，定义了java类被浏览器访问到的规则

将来我们要定义一个类来实现servlet接口 复写他的方法

<!--more-->

### 具体操作步骤：

1.定义一个类  实现servlet的接口

2.实现接口中的抽象方法

3.配置servlet

```xml
<servlet>
  <servlet-name>demo1</servlet-name>
  <servlet-class>cn.coder.jsp.demo1</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>demo1</servlet-name>
  <url-pattern>/demo1</url-pattern>
</servlet-mapping>
```

执行的原理：
1.当服务器接收到客户端浏览器的请求之后，会解析请求的URL路径，获取访问的servlet的资源路径

2.查找web.xml文件，是否有相应的<url-pattern>标签体的内容；

3.如果有，则在找到的相应的<servlet-class>全类名

4.Tomcat会将字节码文件加载进内存 并创建其对象调用其方法



### servlet的执行周期：

1.被创建：执行init方法，只执行一次

2.提供服务：执行servlet方法，执行多次

3.被销毁：执行destroy方法，只执行一次



### 使用servlet3.0 注解配置  

可以不用web.xml配置，通过在类上加@Webservlet("/xxxx")完成配置

#### 注解urlpartten配置：

1. /xxx
2. /xxx/xxx  多层路径  目录结构
3. *.do  *.action  

```java
@WebServlet({"/d2", "/dd2"})
@WebServlet("/xxx/xxx")
@WebServlet("/xxx/*")
@WebServlet("/*")
@WebServlet("*.do")
```



### servlet的体系结构：

servlet接口：

​		— GenericServlet  抽象类

​			将servlet接口中的其他方法做了默认为空的实现，只将service()方法作为抽象

​			将来定义servlet类的实收，直接继承 GenericServlet ，实现service方法即可

​		— httpservlet  抽象类：  对http协议的一种封装，简化操作 **开发常用的**

​			继承httpservlet   复写doGet/doPost方法


### Tomcat+servlet的运作流程：

- Tomcat会根据访问的url中的资源路径，创建相应的servletdemo对象
- Tomcat服务器，会创建request和response对象，request对象中封装请求消息数据
- Tomcat将request和response两个对象传递给service方法，并调用service方法
- 程序员根据请求request，根据response返回响应的数据
- 服务器在给浏览器做出响应之前，会从返回的response对象中拿程序员设置的响应消息数据



