

ResponseBody和RequestBody

@ResponseBody把后台**pojo**转换**json对象**，返回到页面。

@RequestBody接受**前台json**数据，把json数据自动封装**javaBean**





### 准备

导入jackson包  

Jackson-core-asl.jar

Jackson-mapper-asl.jar



添加json转换器

DispatcherServlet-servlet.xml

```xml
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">
  <property name="messageConverters">
    <bean class="org.springframework.http.converter.json.MappingJacksonHttpMessageConverter"/>
  </property>
</bean>

```



### 前端ajax传json到后端控制器

```jsp
<html>
<head>
    <title>注册</title>
    <script src="${pageContext.request.contextPath}/js/jquery-1.8.3.js"></script>
    <script type="text/javascript">
        function a() {
            var inputs = document.getElementsByTagName("input");
            var username = inputs[0].value;
            var password = inputs[1].value;
            $.ajax({
                type: 'post',
                dataType: 'json',
                url: '${pageContext.request.contextPath}/stu/reg.do',
                contentType: 'application/json;charset=utf-8',
                data: JSON.stringify({
                    'username': username,
                    'password': password
                }),
                success: function (resData) {
                    console.log(resData);
                }
            })
        }
    </script>
</head>
<body>
用户名: <input type="text" name="username">
密码: <input type="password" name="password">
<button onclick="a()">json提交</button>
</body>
</html>
```

注意：

.ajax 的data  必须使用JSON.stringify()  处理过的，不然会报错



### 后端接收数据存到 javaBean

```java
 /**
  * 接收json字符串封装成javabean对象
  * 把javabean对象转成json字符串返回
  * @param stu
  * @return
  */
@RequestMapping("/reg")
public @ResponseBody
Student reg(@RequestBody Student stu) {
   System.out.println(stu);
   // 返回json对象
   return stu;
}
```





---------

### 只返回javabean转成的json

```java
/**
 * 只返回json数据
 * @return
 */
@RequestMapping("/reg1")
public @ResponseBody
Student reg() {
  Student stu = new Student();
  stu.setUsername("臭弟弟");
  stu.setPassword("111");
  return stu;
}
```





### 注意

springmvc会自动根据返回的数据类型  设置contenType:"   "

**注意javaBean类一定要提供无参的构造方法**

