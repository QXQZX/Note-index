JSP入门学习：

1.概念：Java Server Pages   java服务端页面

可以理解为一个特殊的界面，  即可以设定html标签  又可以定义java代码

2.原理  ：  jsp 本质上就是一个servlet

3.JSP的脚本：  JSP定义java代码的方式

1. <% 代码 %>   定义的java代码，  在service方法里面  service里面可以定义什么 里面就可以写什么
2. <% 代码 %>  定义的java代码，  在jsp转换后的java类成员变量的位置
3. <%= 代码 %> 定义的java代码，  会输出到界面上   输出语句可以定义什么， 该脚本就可以定义什么



4.  jsp的内置对象

   1. 在jsp页面中不需要获取和创建  直接可以使用的对象   jsp  一共内置了9个对象

   2. request  response

      ​	out：  字符输出流对象。可以将数据输出到页面上  和  response.getWriter()差不多

      response.getWriter()和out.writer()的区别：

      在tomcat服务器真正给客户端做出响应之前，会先找出response的缓冲区数据，再找出out缓冲区数据

      response.getWriter() 数据输出永远在out.write() 之前



















