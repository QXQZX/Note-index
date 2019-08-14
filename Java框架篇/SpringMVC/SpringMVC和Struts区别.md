## 2.4 Spring与Struts的区别【面试题】

### 实现机制：

Struts2是基于过滤器实现的。

Springmvc基于servlet实现。

### 运行速度：

Servlet比过滤器快。

 

Struts2是多例

每一次请求，都会创建一个Action对象

请求来了以后，struts2创建多少个对象：ActionContext，valuestack，UAction，ActionSuport，ModelDriven

 

Springmvc是单例。

​    同一个Controller请求，只会创建一个Controller

 

 

### 参数封装来分析：

Struts基于属性进行封装,Action有参数属性。

Springmvc基于方法封装,参数是写在Controller的方法。

 