语法：

1.xml文档的后缀名  .xml

2.xml第一行必须定义文档声明 声明必须置顶 `<? xml version='1.0' ?>`

3.xml文档中有且仅有一个根标签

4.属性值必须使用引号引起来

5.标签必须正确关闭

6.xml标签名称区分大小写

组成部分：

1.文档声明

​	1.格式 `<? 属性列表 ?>`

​	2.属性列表

​			version：版本号 必须的属性

​			encoding：编码格式  告知解析引擎当前使用的字符集，默认值

​			standalone：是否独立  yes  no

DTD:
	dtd引入：  外部dtd  本地<!DOCTYPE 根标签名 SYSTEM "文件的位置">

​									  本地<!DOCTYPE 根标签名 PUBLIC "文件的名字" "文件的位置">			

Schema(较好)

####解析：

操作xml文档：

​	1.解析(读取)：将文档中的数据读取到内存中

		2. 写入  将内存中的数据保存到xml文档中  持久化储存

解析xml的方式：
1.DOM：将标记语言文档一次性加载进内存，在内存中形成一棵DOM树

​	优点：操作方便  可以对文档进行 CRUD(增删改查)的所有操作

​	缺点：内存占用较大

2.SAX：逐行读取，基于事件驱动 (读一行释放一行  保留出信息)

​	优点：不占内存

​	缺点：只能读取

3.xml常见解析器

​	JAXP:sun公司提供的支持dom，sax  但没人用

​	DOM4J：

​	Jsoup：jsoup 是一款Java 的HTML解析器，可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。

​	PULL：Android操作系统内置的解析器  sax方式的

解析步骤：

```
1.导入jar包
2.获取document对象
3.获取对应的element对象
4.获取数据
```

对象的使用：
	1.jsoup  ： 工具类  可以解析html  xml文档 返回document

2. document  dom树
3. Elements：  元素Element对象的集合  可以当做ArrayList<Element>来使用
4. Element： 元素对象
5. Node  :  结点对象

结点查询：

1. selector选择器  参考select类

2. XPath： 用于xml查询的语法

   ​	导入JsoupXpath的jar包

   