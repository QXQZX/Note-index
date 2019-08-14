# [【JAVA错误笔记】 - c3p0问题java.lang.NoClassDefFoundError:com.mchange.v2.ser.Indirector](https://www.cnblogs.com/Tmc-Blog/p/5797706.html)



错误描述：java.lang.NoClassDefFoundError:com.mchange.v2.ser.Indirector

原因分析：

　　这是c3p0的一个错误信息，我们在下载 c3p0时候，zip压缩包中，有三个jar，其中一个 c3p0-x.x.x.jar，还有一个  mchange.......jar的文件，

该错误原因就是缺少该jar;至于 该jar包的作用就是，一，解决上面的问题，二：本身作用，见，，，jar解压后的源码。

解决方案：

mchange-commons-java-版本号.jar

丢进项目的lib文件即可。

 

回头写下，这几天搭建java框架的感受，以及记录下
springmvc +mybatis框架的

搭建方式一：纯手工的搭建方式，比较传统，但是比较累

搭建方式二：借助类似.net nuget的管理工具 maven方式去搭建，这个比较方便，但是对网速有些要求，你特么的总得下载东西，引用jar包，不然就是配置一下pom.xml就是要卡一大会儿（等待相关插件包下载完成）