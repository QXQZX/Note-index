```javascript
//   开始学习DOM
/*
    Dom  --->  Document  Object  Model
    由浏览器厂商定义  用来操作html和 xml的一类对象的
    集合。 也有人称DOM是对html 和  xml 的标准编程接口
*/
/**
 * test1
 */
// var div = document.getElementsByTagName("div")[0]; // 通过标签名字选中
// div.style.width = "100px";
// div.style.height = "100px";
// div.style.backgroundColor = "red";

// var cnt = 0;
// // 点击后变化
// div.onclick = function () {
//     this.style.backgroundColor = (cnt % 2 == 0) ? "green" : "red";
//     cnt++;
// }

/**
 * test2
 */
// var btn = document.getElementsByTagName("button");
// var div = document.getElementsByClassName("content");

// for (var i = 0; i < btn.length; i++) {  
//     // 使用了闭包的特性
//     (function (n) {
//         btn[i].onclick = function () {
//             for (var j = 0; j < btn.length; j++) {
//                 btn[j].className = "";
//                 div[j].style.display = "none";
//             }
//             this.className = "active";console.log(i);
//             div[n].style.display = "block";

//         }
//     }(i))
// }

/**
 * 方块的移动
 */

// var div = document.createElement("div");

// document.body.appendChild(div);
// div.style.height = "100px";
// div.style.width = "100px";
// div.style.backgroundColor = "green";
// div.style.position = "absolute";
// div.style.left = "0";
// div.style.top = "0";

// // 每50ms移动一次
// // setInterval(function () {
// //     div.style.top = parseInt(div.style.top) + 2 + "px";
// //     div.style.left = parseInt(div.style.left) + 2 +"px";
// // }, time);
//   time 不可更改



// // 鼠标控制的移动
// document.onkeydown = function (e) {
//     switch (e.which) {
//         case 38:
//             div.style.top = parseInt(div.style.top) - 15 + "px";
//             break;
//         case 40:
//             div.style.top = parseInt(div.style.top) + 15 + "px";
//             break;
//         case 37:
//             div.style.left = parseInt(div.style.left) - 15 + "px";
//             break;
//         case 39:
//             div.style.left = parseInt(div.style.left) + 15 + "px";
//             break;

//     }
// }


/** 
 * 选择器
 * 
*/
// 实时的
document.getElementById('') //  
document.getElementsByName() // 选择这种<a name=""></a>
document.getElementsByTagName()  // 通过标签名
document.getElementsByClassName() // 类名

// 静态的 选出来是副本
document.querySelector('div > span > strong.demo') // css选择器 ie7及以下没有
document.querySelectorAll() // 同上
/*  遍历结点树
Node.parentNode    // 求结点的父节点
childNodes   //  子节点们  []
firstChild   //  第一个子节点
lastChild    //  最后一个子节点
nextSibling  //  后一个兄弟结点
previousSibling  // 前一个兄弟结点
*/
/* 遍历元素结点树 <=ie9  不兼容
parentElement // 元素父节点
children // 元素子节点
childElementCount // 子节点个数
firstElementChild  
lastElementChild
nextElementSibling
previousElementSibling
*/

/* 结点的四个属性
nodeName  //  只读  
hasChildNodes();
nodeType
nodeValue

*/

/*
创建
div.innerHTML = '123';  在div中添加123  文本
div.innerText
document.creatElement('')  // 创建一个元素结点
document.creatTextNode('')  // 创建文本结点
插入
ParentNode.appendChild('')  // 插入子节点 （ 剪切<把已有元素添加> 或 直接添加 ）
document.body.appendChild('')  
ParentNode.insertBefore(a, b)  // parent 在b之前 插入a 
删除
parent.removeChild(); // 剪切出来  可以  var ii = ....
child.remove();   // 自己销毁
替换
parentNode.replaceChild(new, origin);
结点方法：
div.setAttribute('class', 'demo');   设置属性
div.getAttribute('demo');   // 获得属性


可直接
div.className('')  来设置类名
div.id('');
 */

/*
js  定时器
var timer = setInterval(function() {
    if () {
        clearInterval(timer);
    }


}, time)


var timer = setTimeout(function() {

    console.log('a');
}, 1000);

clearTimeout();

*/

```

