response对象：

功能： 设置响应消息

 	1. 设置响应行
      	
      	
      
      1. 格式  HTTP/1.1 200 OK
      
   2. 设置状态码  setStatus()         404 200 302 301

 	2. 设置响应头
      	
      	setHeader(String name, String name)  
       
       `response.setHeader("Content-Type", "text/html;charset=utf-8");`
        response对象中对Content-Type响应头进行了封装,可以使用一下代码代替 上面的
        如果设置了Content-Type,服务器会自动的设置 characterEncoding,因此解决乱码只需要设置Content-Type响应头一行代码就可以了,但是为了代码的可读性更高,一般还是建议同时设置 characterEncoding 和 Content-Type.
        ` response.setContentType("text/html;charset=utf-8");`
       
  4. 设置响应体

       1. 使用步骤：  获取输出流：getWriter()   getOutputStream()

案例：

#### 重定向：

代码实现

```java
// 设置状态码
resp.setStatus(302);
// 设置响应头location
resp.setHeader("location", "/test/resdemo2");

// 简单的方式
resp.sendRedirect("/test/resdemo2");
```

重定向的特点：redirect

​	1.地址栏发生变化

​	2.重定向可以访问其他站点的资源

​	3.重定向是两次请求  所以不能用request来共享对象

转发的特点：forward

​	1.转发地址栏路径的变化

​	2.转发只能访问当前服务器下的资源

​	3.转发只是一次请求



服务器输出**字符**数据到浏览器：

```java
resp.setCharacterEncoding("utf-8"); // 设置编码 UTF-8
//resp.setHeader("Content-type", "text/html;charset=utf-8");  // 告诉浏览器解码 是 UTF-8  默认是GBK

// 简写： 一定要在获取流之前 设置编码
resp.setContentType("text/html;charset=utf-8");

// 获取输出流  printWriter可以实现自动刷新
PrintWriter pw = resp.getWriter();  // 该流的默认编码是  ISO-8859-1
pw.write("<h1>hello 张</h1>");  // 可以写标签
```

服务器输出**字节**数据到浏览器：

```java
resp.setCharacterEncoding("utf-8"); // 设置编码 UTF-8
resp.setContentType("text/html;charset=utf-8");
// 获取输出流  不能实现自动刷新
ServletOutputStream so = resp.getOutputStream();
so.write("你好".getBytes("utf-8"));
```

注意：  字节输出流和字符输出流只能获取一个







案例2：

实现  验证码图片随机生成功能

1.创建对象  验证码图片对象

2.美化图片

3.将图片展示到页面上



   