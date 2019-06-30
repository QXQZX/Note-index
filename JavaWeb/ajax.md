1.原生js实现

```javascript
function func() {
  // 1.创建对象
  var xmlhttp;
  if (window.XMLHttpRequest) {// code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp = new XMLHttpRequest();
  } else {// code for IE6, IE5
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
  // 2、建立连接
  /*
  	参数：
    1、请求方式   GET  POST                
			get方式，请求参数在url后面拼接  send为空参
    	post方式，请求参数在send方法中定义
      2、请求的url          
      3、同步请求： true：异步   false：同步
	*/
  xmlhttp.open("get", "../ajaxServlet?name=张国辉&msg=你好", true);
  xmlhttp.send();

  // 3.响应结果  xmlhttp.responseText
  // 当xmlhttp响应状态改变时 会触发此函数
  xmlhttp.onreadystatechange = function () {
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
      document.getElementById("myDiv").innerHTML = xmlhttp.responseText;
      alert(xmlhttp.responseText);
    }
  }
}
```





2.jquery实现

```javascript
$.ajax({
  url: "../ajaxServlet",
  type: "POST",
  data: {
    "name": "张国辉",
    "msg": "你好"
  },
  success: function (data) {//响应成功的回调函数
    // data是服务器的响应值
    alert(data);
  },
  error: function () {
    alert("出错了、、、")
  },
  dataType: "json"
});
```



还有

$.get()

$.post()