常见的JSON解析器：

Json-lib  Gson  fastjson  jackson



1.json转为java对象



2.java对象转为json

使用步骤：  

​	1.  导入jackson的相关的jar包

 	2. 创建Jackson核心的对象  ObjectMapper
 	3. 调用ObjectMapper的相关的方法进行转换
      	1. writerValue(参数1, obj)      百度查文档
      	2. 注解
           	1. @JsonIgnore：  排除属性。  在类里的成员变量里添加
           	   2. @JsonFormat(pattern = "yyyy-MM-dd")  格式化属性
 	5. 复杂java对象的转换      List数组           Map

 