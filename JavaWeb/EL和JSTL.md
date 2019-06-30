### EL表达式：

1.概念：Expression Language  表达式语言

2.作用：替换和简化jsp页面中的java代码的编写

3.语法： ${表达式}

4.注意：jsp默认是支持el表达式的  如果要想忽略el表达式

​		1.设置 jsp中的page指令中：  isELIgnored="true"  忽略当前jsp中的所有的el表达式

​		2.\${表达式}  ：  忽略这个el表达式



5.使用：

​	1.运算

​		运算符：  百度搜。。。。。

​		特殊的：空运算符  empty

​				功能：  用于判断字符串、集合、数组对象是否为null并且长度是否为0     

​				${empty list}    判断字符串集合数组对象是否为null  或者长度为0      

​		        ${not empty list}   与上面相反

​	2.获取值

​		1.el表达式只能从域对象中获取值

​		2.语法  

​		`${域名称.键名}` 从指定域中获取值    

​		 `${键名}`  表示依次从最小的域中查找是否有该键对应的值，直到找到为止

​			1.pageScope        —> pageContext

​			2.requestScope	—> request

​			3.sessionScope 	—> session

​			4.applicationScope	—> application (ServletContext)

​		3.获取对象、List集合、Map集合

​			1.对象：  ${域名称.键名.属性名}   这里的属性名是setter | getter方法去掉  set|get  将剩余的部分首字母变小写

​					getName  —> Name —> name

​			2.List集合：    ${域名称.键名[索引]}

​			3.Map集合：  

​				${域名称.键名.key名称}   

​				${域名称.键名.["key名称"]}  

​	

​	3.隐式对象

​		el表达式中的11个隐式对象

​		pageContext ：   用于获取其他八个内置对象

​			    ${pageContext.request.contextPath}  :   动态获取虚拟目录





---------------



### JSTL

1.概念：JavaServer Pages Tag Library       JSP标准标签库     apache出品开源免费

2.作用：用于简化和替换jsp界面上的java代码

3.使用步骤：

​	1.导入jstl相关的jar包

​	2.使用taglib指令引入 标签库

​	3.使用标签







