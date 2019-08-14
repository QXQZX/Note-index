通过model对象回显数据

Controller 

```java
@RequestMapping("/list")
public String list(Model model) {
  User user = new User();
  user.setUsername("臭弟弟");
  user.setPassword("123");

  model.addAttribute("u", user);
  return "user/userList";
}
```

前端界面获取

```jsp
<body>
  ${u.username}<br>
  ${u.password}<br>
</body>
```





--------------



URL映射模板：

配置接收url模版映射
{}:  匹配接受页面Url路径参数
**@Pathariable**：{}里面参数注入后面参数里面

### Restful:  风格的mapper映射



web.xml  添加

```xml
<!--restful风格-->
<servlet-mapping>
  <servlet-name>DispatcherServlet</servlet-name>
  <url-pattern>/restful/*</url-pattern>
</servlet-mapping>
```



controller层：

```java
// 多参数 继续添加 "/edit/{id}/{name}/{age}"
@RequestMapping("/edit/{id}")
public String edit(@PathVariable int id, Model model) {
  User user = new User();
  user.setUsername("小弟弟");
  user.setPassword("id:" + id);

  model.addAttribute("user", user);
  return "user/edit";
}

```



Jsp  调用：

```jsp
<a href="${pageContext.request.contextPath}/restful/user/edit/${233}">编辑</a>
```

