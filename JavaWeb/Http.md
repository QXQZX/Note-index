HTTP:

**传输协议：**定义了客户端和服务端的通信，发送数据的格式

**特点：**

1.给予TCP/IP的高级协议

2.默认端口是80

3.给予请求/响应模型的：  一次请求对应一次响应

4.无状态的：每次请求之间的相互独立，不能交互数据

<!--more-->

### 请求消息的数据格式

​	1.请求行

​	客户端：

​			请求方式   请求的url  请求的协议/版本

​			POST    /xxx.html     HTTP/1.1 

​	服务端：

​			请求的协议/版本  响应状态码 响应结果

​			HTTP/1.1   200   OK  

​	状态码

​	状态代码为3位数字。
​	1xx：指示信息--表示请求已接收，继续处理。
​	2xx：成功--表示请求已被成功接收、理解、接受。
​	3xx：重定向--要完成请求必须进行更进一步的操作。
​	4xx：客户端错误--请求有语法错误或请求无法实现。
​	5xx：服务器端错误--服务器未能实现合法的请求。



​	2.请求头：  客户端浏览器 告诉服务器一些信息

​			格式：   请求头的名称：  请求头的值

```
HTTP响应中的常用响应头(消息头)
　　Location: 服务器通过这个头，来告诉浏览器跳到哪里
　　Server：服务器通过这个头，告诉浏览器服务器的型号
　　Content-Encoding：服务器通过这个头，告诉浏览器，数据的压缩格式
　　Content-Length: 服务器通过这个头，告诉浏览器回送数据的长度
　　Content-Language: 服务器通过这个头，告诉浏览器语言环境
　　Content-Type：服务器通过这个头，告诉浏览器回送数据的类型
　　Refresh：服务器通过这个头，告诉浏览器定时刷新
　　Content-Disposition: 服务器通过这个头，告诉浏览器以下载方式打数据
　　Transfer-Encoding：服务器通过这个头，告诉浏览器数据是以分块方式回送的
　　Expires: -1 控制浏览器不要缓存
　　Cache-Control: no-cache
　　Pragma: no-cache
```

​			Referer： 记录请求地址  从哪来的请求

​						作用：  1.防盗链  2.统计工作

​	3.请求空行  

​			 分割post的请求头和请求体

​	4.请求体正文

```
封装post请求消息的请求参数的

```



GET  请求的参数在请求行中  url长度有限制

POST  请求的参数在请求体中  长度无限制

#### 客户端请求格式

```http
POST /hello.txt HTTP/1.1
User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
Host: www.example.com
Accept-Language: en, mi
```



#### 服务器响应消息的格式

```http
HTTP/1.1 200 OK   // 响应行  用于描述副武器的请求处理结果
Server: Apache-Coyote/1.1
Content-Type: text/html;charset=ISO-8859-1   //这四行 是消息头
Content-Length: 105
Date: Tue, 27 May 2014 16:23:28 GMT

<html>
<head>
<title>Hello World JSP</title>
</head>
<body>
		Hello World!
</body>
</html>

```







