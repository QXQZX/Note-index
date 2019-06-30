SpEL表达式

```xml
<property name="" value="#{表达式}" />
<!--
	#{123} #{"jack"}  数组 字符串
	#{beanID} || ref="beadID"  另一个bean的引用
	#{beadID.propName}  操作数据
	#{beanID.toString()}  执行方法
	#{T(类).字段|方法}  静态方法 字段    #{T(java.lang.Math).PI}
-->
```

