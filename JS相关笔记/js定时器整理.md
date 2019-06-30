# js定时器整理(执行一次、重复执行)

在javascritp中，有两个关于定时器的专用函数，分别为：

​	1.倒计定时器：timename=setTimeout("function();",delaytime);

​	2.循环定时器：timename=setInterval("function();",delaytime);

第一个参数“function()”是定时器触发时要执行的动作，可以是一个函数，也可以是几个函数，函数间用“；”隔开即可。



比如要弹出两个警告窗口，

便可将   “function();”   换成    “alert('第一个警告窗口!');alert('第二个警告窗口!');”；

而第二个参数“delaytime”则是间隔的时间，以毫秒为单位，即填写“5000”，就表示5秒钟。 　　



**倒计时定时器**， 是在指定时间到达后触发事件;  **而循环定时器**，就是在间隔时间到来时反复触发事件，

**两者的区别在于：前者只是作用一次，而后者则不停地作用。**

比如你打开一个页面后，想间隔几秒自动跳转到另一个页面，则你就需要采用

`倒计定时器  “setTimeout("function();",delaytime)” `

而如果想将某一句话设置成一个一个字的出现， 则需要用到

`循环定时器  “setInterval("function();",delaytime)” `



定时器：用以指定在一段特定的时间后执行某段程序。

JS中定时执行,setTimeout和setInterval的区别,以及l解除方法

* setTimeout(Expression,DelayTime),在DelayTime过后,将执行一次Expression, setTimeout 运用在延迟一段时间，再进行某项操作。 setTimeout("function",time) 设置一个超时对象

* setInterval(expression,delayTime),每个DelayTime,都将执行Expression.常常可用于刷新表达式. setInterval("function",time) 设置一个超时对象

**SetInterval为自动重复，setTimeout不会重复**

清除：

* clearTimeout(对象) 清除已设置的setTimeout对象 
* clearInterval(对象) 清除已设置的setInterval对象

 

下面是两种函数的格式：

1.

```html
<script> 
//定时器 异步运行 
  function hello(){ 
  	alert("hello"); 
  } 
  //使用方法名字执行方法 
  var t1 = window.setTimeout(hello,1000); 
  var t2 = window.setTimeout("hello()",3000);//使用字符串执行方法 
  window.clearTimeout(t1);//去掉定时器 
</script>
```

2.

```html
<script> 
  function hello(){ 
    alert("hello"); 
  } 
  //重复执行某个方法 
  var t1 = window.setInterval(hello,1000); 
  var t2 = window.setInterval("hello()",3000); 
  //去掉定时器的方法 
  window.clearInterval(t1); 
</script> 
```

