### request的功能：

#### 1.获取请求消息数据：

​	1.获取请求行数据

​		GET /xxx/xxx/demo1?name=zhang HTTP/1.1

​		方法

```java
String getMethod() // 获取请求方式 GET/POST
*String getContextPath() // 获取虚拟的目录
String getServletPath() // 获取servlet的路径
String getQueryString() //获取get方式的请求参数
*String getRequestURI() // /xx/xxx/xx   URI 统一资源标识符
String getRequestURL()  // http://xxx.com/dd/cc  URL  统一资源定位符
String getProtocol() // 获取协议的版本
```

#### 2.获取请求头数据

方法：

```java
String getHeader(String name)  // 通过请求头的名称获取请求头的值
getHeaderNames()  // 获取所有请求头的名称
```

#### 3.获取请求头数据

请求体：只有post请求方式 才有请求体，在请求体中封装了post请求的请求参数

步骤：
	1.获取流对象  

​           BufferedReader getReader() :  获取字符输入流  只能操作字符数据

​		   ServletInputStream getInputStream()  获取字节输入流，可以操作所有类型的数据

​	2.再从流对象这种拿数据

#### 4.其他的方法功能

1.获取请求参数的通用方式

```java
String getParameter(String name) // 根据参数的名称获取参数值
String[] getparameterValues(String name) // 根据参数的名称获取参数值得数组  用于复选框
Enumeration<String> getParameterNames() // 获取所有请求的参数名称
Map<String String[]> getParameterMap()  // 获取所有参数的map集合
```

中文乱码问题：

get方式：  tomcat 8 已经将get方式乱码问题解决了

post方式： 会乱码：

​	解决：在获取参数之前  设置request的编码问题：request.setCharacterEncoding("utf-8");

2.请求转发：  一种在服务器内部的资源跳转方式

  1. 步骤：

     ​	通过request对象获取请求转发器对象RequestDispatcher rd = req.getRequestDispatcher(String path).

     ​	使用对象进行转发： rd..forward(req, resp);

     ​	链式写法：req.getRequestDispatcher("/d2").forward(req, resp);

		2. 特点：

     ​	浏览器的地址栏路径不会改变

     ​	只能转发到当前服务器内部资源

3.共享数据：

域对象：一个有作用范围的对象，可以小范围的共享数据  

request域：  代表一次请求的范围，   一般用于请求转发的多个资源的共享数据

方法：

``` java
void setAttribute(String name, Object obj) // 存储数据
Object getAttribute(String name)  // 通过键获取数据
void removeAttribute(String name)  // 通过键移除键值对
```

4.获取ServletContext

​	ServletContext getServletContext();

