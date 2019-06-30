### 一、jQuery.fn.method()=function(){}  和  $.fn.extend({})  的比较

jQuery.fn === jQuery.prototype

**1.$.fn.method() = function() {} 的调用方法  扩展到了对象的prototype上， 所以实例化了一个jQuery对象的时候，他就具有了这些方法。**

比如：

```javascript
$.fn.myExtension = function(){
 var currentjQueryObject = this;
 //work with currentObject
 return this;//you can include this if you would like to support chaining
};
```

```javascript
$.fn.blueBorder = function() {
  this.each(function() {
    $(this).css({
			"border":"1px solid blue"
    });
  });
  return this;
}
// 由于有 return this; 所以是支持链式写法的
$('.blue').blueBorder().blueText();
```

2. `$.fn.extend({},{},{}...)` 是对 `$.fn.method()= function(){} `的扩展支持 **扩展多个对象**  可以定义多个方法：

```javascript
$.fn.extend({
	a : function() {},
  b : function() {},
  c : function() {}
});
// 调用
$().a();
```

等效于：

```javascript
$.fn.a = function() {};
$.fn.b = function() {};
$.fn.c = function() {};
```

$.extends({}), 可以理解为为jQuery 添加 扩展的静态方法

如：

```javascript
$.extend({ 
　　add : function(a,b) {return a+b;} 
});

$.add(3,4); //return 7 
```





### 二、return this.each()  的使用

Demo1:

```HTML
<div class="test">
	div1
</div>
<div class="test">
	div2
</div>
<script type="text/javascript">
		$.fn.addStr = function(str){
			this.each(function(){
				this.innerHTML = str;
			});
		}
	var obj = $(".test").addStr("add str");//obj is undefined
	alert(obj instanceof jQuery);//false
</script>

<!--此时，我们得到的obj是undefined,也就是说如果我们想链式调用是不行的，如 :$(".test").addStr("add str").css("color","red")-->
```

demo2:

````html
<div class="test">
	div1
</div>
<div class="test">
	div2
</div>
<script type="text/javascript">
		$.fn.addStr = function(str){
			return this.each(function(){
				this.innerHTML = str;
			})
		}
	var obj = $(".test").addStr("add str").css("color","red");
  //现在我们可以继续调用jquery对象的方法.css("","");
	alert(obj instanceof jQuery);//true
 </script>
<!-- 而现在，我们能够取得返回的jquery对象，可以进行链式调用。 -->
````

