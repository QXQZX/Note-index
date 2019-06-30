1.指令

作用：  用于配置jsp页面，导入资源文件

格式： <%@ 指令名称 属性名1=属性值1  属性名2=属性名2 ….%>

分类：

​	1.page：   配置jsp界面的

​		contentType：  等同于response.setContentType()  设置响应体的字符集和mime类型

​		pageEncoding： 设置当前界面的字符集

​		import：导包

​		errorPage： 当页面发生异常后，会自动跳转到指定的错误界面

​		isErrorPage：表示当前界面是否为错误界面

​			true：是，可以使用内置对象exception  		false：默认



​	2.include：  页面包含的。  导入页面的资源文件

​		<%@include file="top.jsp" %>

​	3.taglib：  导入资源

​		<%@ taglib prefix="c" uri="http://xxxxxxxx.com/jsp/jstl/core" %>     prefix是前缀 



2.注释

​	1.html注释  <!---->  只能注释  html代码片段

​	2.jsp注释：  推荐使用  <%— —%>  可以注释所有



3.内置对象：  在jsp界面中不需要创建，直接使用的对象



#### 九个内置对象

| 变量名      | 真实类型            | 作用                                         |      |
| :---------- | :------------------ | :------------------------------------------- | ---- |
| pageContext | PageconText         | 当前页面共享数据，还可以获取其他八个内置对象 |      |
| request     | HttpServletRequest  | 一次请求访问的多个资源(转发)                 |      |
| session     | HttpSession         | 一次会话的多个请求间共享                     |      |
| application | ServletContext      | 所有用户间共享(服务器关闭后停止)             |      |
| response    | HttpServletResponse | 响应对象                                     |      |
| page        | Object              | 当前界面的Servlet对象  this                  |      |
| out         | JspWriter           | 输出对象，数据输出到页面上                   |      |
| config      | ServletConfig       | servlet的配置对象                            |      |
| exception   | Throwable           | 异常对象                                     |      |
|             |                     |                                              |      |

