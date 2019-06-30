回话技术：
	Cookie  和  session



1.会话： 一次会话中包含多次请求和响应

一次会话：浏览器第一次给服务器资源发送请求，会话建立，知道有一方断开为止

2.功能：在一次会话范围内的多次请求之前，共享数据

3.方式：

​	1.客户端会话技术 Cookie

​	2.服务端会话技术  Session

### Cookie

1.概念：    客户端会话技术，将技术保存到客户端

2.使用步骤

​	1.创建Cookie对象，绑定数据

​		new Cookie(String name, String value)

​	2.发送Cookie对象

​		response.addCookie(Cookie cookie)

​	3.获取Cookie，拿到数据 遍历

​		Cookie[] request.getCookies() 

####Cookie的工作原理：

1.客户端发送请求到服务器

2.服务器创建cookies通过response做出响应，这时响应头会有一句 set-cookie: xxx=xxx   (xxx=xxx是cookie数据)

3.客户端浏览器会把cookie数据保存到客户端浏览器上

4.当第二次请求的时候，浏览器会生成一个消息头 cookie: xxx=xxx 发送到浏览器



#### Cookie的细节

1.一次可以发送多个cookies

2.cookies在浏览器中的储存时间

​	1.默认情况下，浏览器关闭后，cookie数据被销毁

​	2.持久化储存

​		setMaxAge(int seconds)   

​			正数(将cookies数据写到硬盘文件中)  

​			负数(默认值) 

​			0(删除)

3.cookie能不能存中文的问题

​	在tomcat8之前，不可以  需要用URLDcoder  URLEcoder进行编码解码

​	tomcat8 之后  cookie支持中文数据  但特殊字符还是不能支持， 建议使用URL编码存储  URL解码

4.cookie共享问题

​	1.假设在一个tomcat服务器中部署了多个web项目，那么这些cookie能不能共享呢？

​			 默认情况下是不能共享的

 			可以通过setPath(String path):  设置cookie的范围默认情况下设置**当前的虚拟目录**  如果要共享，设置setPath("/")

​	

 2. 不同的tomcat服务器之间共享cookie问题

     1. setDomain(String path)  如果设置一级域名相同，那么多个服务器之前可以共享cookie

        ​	例如： setDomain(".baidu.com"),  那么tieba.baidu.com  和 news.baidu.com中cookie可以共享

​			 

5.cookie的特点和作用

​	1.cookie储存数据在客户端浏览器

​	2.浏览器对于单个cookie的大小限制(4kb)  以及 同一个域名下的cookie数量有限制(20个)

​	

​	作用：cookie一般用于储存少量的不太敏感的数据

​			在不登录的情况下，完成服务器对客户端的身份识别





6.案例：记录上一次的访问 时间

需求： 访问一个servlet 如果是第一次访问， 则提示您好您是第一次 访问；

如果不是，则提示欢迎回来，你的上次访问的时间是

分析：

​	可以采用cookie来完成

​	在服务器中 的 servlet中有一个  判断是否名为lasttime的cookie

​		有： 不是第一次访问， 欢迎回来。。。。  写回cookie lasttime=xxxx

​		没有： 响应数据，  您好，欢迎您首次访问  写回cookie  lasttime=xxxxxxxxx







### Session



1.概念：服务器会话技术，在一次会话的多次请求间共享数据，将数据保存到服务端对象中。  HttpSession

2.快速入门：

​    获取HttpSession对象：  HttpSession session = request.getSession();

​	使用HttpSession对象： 

``` java
Object getAttribute(String name)
void setAttribute(String name, Object value)
void removeAttribute(String name)
```

3.原理： session的实现原理是依赖于cookie的



4.细节：

​	1.当客户端关闭，服务器不关闭，两次session是否为同一个

​		默认：不是

​		改变默认，可以通过穿件cookie，键为JSESSIONID，设置最大的存活时间，让cookie持久化储存

```java
HttpSession session = req.getSession();
System.out.println(session);
// 关闭客户端后 仍能访问该session
Cookie cookie = new Cookie("JSESSIONID", session.getId());
cookie.setMaxAge(60 * 60);
resp.addCookie(cookie);
```

​	

​	2.客户端不关闭，服务器关闭，两次session是否为同一个

​		不是同一个，但是要确保数据不丢失

​			session的钝化： 在服务器正常关闭之前，将session序列化到硬盘上

​			session的活化：在服务器启动之后，将session文件转化为内存中的session对即可

​		session的钝化和活化由tomcat完成，(idea不能实现)

​	

​	3.session的失效时间：

​		1.服务器关闭

​		2.session对象调用invalidate()

​		3.session修改默认的失效时间  30min

选择性配置

```xml
<session-config>
	<session-timeout>30</session-timeout>
</session-config>
```



5. session的特点：

   ​	1.session用于储存一次绘画的多次请求数据，存在服务器

   ​	2.session可以存任意类型的数据，任意大小的数据

6. session与cookie的区别

   1. session存储的数据在服务器端，cookie在客户端
   2. session没有数据大小的限制， Cookie有
   3. session数据安全， cookie相对不安全



​	