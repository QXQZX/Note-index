ServletContext对象：

1.概念代表整个web应用，可以和程序的容器(服务器)来通信

2.获取：

1.通过request对象获取：

​	request.getServletContext();

​	this.getServletContext();

3.功能：

​	1.获取MIME类型：

​		MIME类型：  在互联网通信工程中定义的一种文件的数据类型

​		格式：大类型/小类型    例如：  text/html     image/jpeg

​		获取MIME的方法：

​		String getMimeType(String file)

​	2.域对象：共享数据

​		ServletContext的对象范围：  所有用户的请求数据  自tomcat启动 到  关闭

```java
void setAttribute(String name, Object obj) // 存储数据
Object getAttribute(String name)  // 通过键获取数据
void removeAttribute(String name)  // 通过键移除键值对
```



​	3.获取文件的真实(服务器)路径

​		String getRealPath(String path);

```java
// 获取文件的服务器(真实)路径
String s1 = sc.getRealPath("/a.txt"); // web目录下的资源访问
System.out.println(s1);

String s2 = sc.getRealPath("WEB-INF/a.txt");// WEB-INF目录下的资源访问
System.out.println(s2);

String s3 = sc.getRealPath("WEB-INF/classes/a.txt");// src目录下的资源访问
System.out.println(s3);
```



