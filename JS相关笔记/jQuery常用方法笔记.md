#学过的jQuery方法：

1.`$(":text")`   选取所有 type="button" 的 <input> 元素 和 <button> 元素

2.`.end()`方法   详查文档

3.`.map()`方法  返回一个对象  详查文档

4.`.append()` 向结点中插入内容   详查文档

5.`.html()`  返回结点的内部的HTML内容字符串

6.`.val()`  放回标签的value值

7.`.get()` 方法允许我们直接访问jQuery对象中隐含的DOM节点   通过索引获取

​		`console.log( $( "li" ).get(0) );`等价于`console.log( $( "li" )[0] );`

8.`$(".a").find(".b")` 方法 查找子元素  如 选出div.a  下的  div.b

9.`.data("")` 方法  用于自定义标签的属性

​	如：

```html
<div class="filled" data-width="95%"></div>
<script>
	var width = $("filled").data("width"); // "95%"
  
</script>
```







