面向对象   继承  原型原型链

```javascript


//  对象的创建方法
//   1、  var obj = {}  plainObject  对象字面量
//    2、 构造函数
//<1>系统 自带构造函数
var obj = new Object(); // 执行一次生成一个
// 比如 Array()  Number()

// <2>自定义构造函数  大驼峰式构造规则  
function Person() {
    // 先隐式生成 this 对象（构造函数内部原理）
    // var this = {
    //     name : "",
    //     age : ,
    //     height : ,
    // }

    this.name = "dsb";
    this.age = 18;
    this.height = 60;
    this.run = function () { };

    // 最后隐式返回
    // return this;
}
var person1 = new Person();

// 或者
function Person1(name, height) {
    var that = {};
    that.name = name;
    that.height = height;
    return that;
}


// 2. 包装类  new Boolean()  new String()  new Number

var num = 4;  // 原始值
num.len = 3;
/* 隐式生成  new Number(4).len = 3;
 生成之后  js觉得他不对  然后他帮你删除  delete*/
console.log(num.len);
// 当你再次访问的时候  他会再次帮你生成  
// new Number(4).len = undefined;

// 然而

var str = "aaaa";
str.length = 2;
//  new String("aaaa").length = 2  delete

console.log(str.length); // 4
// 会有 new String("aaaa").length = 4;



// 3.原型   原型链  call / apply
// 当unicode > 255 那么该字节的长度为2  <= 255 为1

// Person.prototype     ---  原型
// Person.prototype = {  name : "sss", age : 22  }  --- 是祖先
// 所有new 出来的Person对象都有它的属性
/*
    原型定义：  原型是function对象的一个属性，他定义了
    了构造函数制造出的对象的公共祖先。通过该构造函数产生的
    对象，可以继承该原型的属性和方法。  原型也是对象。
*/
Person.prototype = {
    LastName : "zhang",
    name : "ming",
    say : function () {
        console.log("hehe");
    }
}
function Person(name) {
    this.LastName = name;  // 会覆盖该对象继承自原型的东西

}
var p = new Person("aa");

/*而如果执行  p.name = "sss";  不会修改原型的值  而是会在
对象内加一个name  属性

修改原型属性的正确姿势：
Person.prototype.name = "mingming";

不能通过delete删除对象原型属性  来删除 原型属性
delete p.prototype.name   不会动原型的
delete Person.prototype.name   这样会动原型的

*/

function Person() {
    /*
    var this = {


        __proto__ : Perosn.prototype
    }
    */

}

var obj = {};
var p = new Person();
p.__proto__ = obj; // 改遍原型


// 实例
Person.prototype = {
    name: "a",
    sayName: function () {
        console.log(this.name);
    }
}
function Perosn() {
    this.name = "b";
}

var person = new Person();
person.sayName(this.name); // 输出b    this指的是  person  
person.prototype.sayName(this.name); // 输出a  this指的是person.prototype


// call在开发中的使用
// 轮子生产车间
function Wheel(wheelSize, style) {
    this.wheelSize = wheelSize;
    this.style = style;
}
// 样式设计车间
function Sit(sitColor) {
    this.sitColor = sitColor;
}
// 框架生产车间
function Model(height, width, len) {
    this.height = height;
    this.width = width;
    this.len = len;
}
// 汽车组装车间
function Car(wheelSize, style, sitColor, height, width, len) {
    Wheel.call(this, wheelSize, style);
    Sit.call(this, sitColor);
    Model.call(this, height, width, len);
}

var car = new Car(100, "花里胡哨", "red", 1000, 1500, 5000);

var obj = {
    a : 1,
    b : 2,
    c : 3,
    __proto__ : {
        d : 444
    }
}
for (var prop in obj) {
    console.log(obj[prop]); // 1 2 3 444
}
// 忽略原型中的东西
for (var prop in obj) {
    if (obj.hasOwnProperty(prop)) {
        console.log(obj[prop]); // 1 2 3
    }
}
// in
// 判断 属性是否在obj中（ 包括原型中的 ）
if ('a' in obj) {}  //返回bool 
// instanceof
// 判断 返回true/false  
person instanceof Person  // person对象是否是Person构造出来的
```

