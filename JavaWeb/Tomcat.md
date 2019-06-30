软件分为以下的两种：

* C/S    客户端  服务器

* B/S     浏览器  服务器

JavaEE：  Java语言在企业级开发中的使用的技术规范的总和  一共规定了13项大的规范

Web 服务器软件：
 服务器：  安装了服务器软件的计算机

服务器软件：接受用户请求 处理请求  做出响应

web服务器软件: 接受用户的请求  处理请求  做出响应  部署web项目  让用户通过浏览器来访问

常见的java相关的web服务器软件：

1.weblogic： orcale的  大型的javaee服务器  支持所有的Javaee规范  收费！！！

2.webSphere： IBM的  大型的javaee服务器  支持所有的Javaee规范  收费！！！

3.JBOSS： JBOSS的  大型的javaee服务器  支持所有的Javaee规范  收费！！！

4.Tomcat ： Apache基金组织  中小型JavaEE服务器  仅仅支持少量的JavaEE规范servlet/jsp  开源免费



Tomcat安装： 从官网下载相应的压缩包，然后解压即安装完成

Tomcat目录结构：
—  bin 可执行的文件

— conf   配置文件

— libs  依赖jar包

— logs  日志文件

— temp  临时文件

— webapps  存放web项目

— works   存放运行时的数据



一般会将Tomcat的端口号改成80  因为他是http的默认端口  不写端口号 只写ip就能访问



部署方式：
1.直接将项目放到webapps下

* /xxxx  直接复制文件夹

* Tomcat会 自动的 识别 解压  删除xxx.war格式的包  war打包工具

2.通过修改conf/server.xml  (不建议使用)

在server.xml中的<Host>标签下添加

```xml
<Context docBase="/xxx/xxxx" path="/hehe" /> 
<!--docBase是真实的路径  path是虚拟路径(指定的访问路径 可以不存在)-->
```

2.通过在conf/Catalina/创建任意名称的xml  例如abc.xml  (建议使用)

在abc.xml中的<Host>标签下添加

```xml
<Context docBase="/xxx/xxxx"/> 
<!--docBase是项目真实的路径-->
```

以后就可以直接通过127.0.0.1:8080/abc来访问资源了



动态项目目录结构

— /根目录

​	 — /WEB-INF目录

​			— web.xml  web项目的核心配置文件

​			— classes目录：放置字节码文件的目录

​			— lib目录：防止依赖的jar包