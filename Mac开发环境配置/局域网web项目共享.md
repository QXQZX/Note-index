# Mac系统，同局域网内，别人电脑访问我本地项目的方法

### 主要分为三个步骤：

**第一步：获取本Mac的ip地址在局域网下分配的ip**

方法：

```bash
# 终端输入
$ ifconfig | grep "inet"
# 找里面 192.168.xx.xxx 字样
```

如：我的ip地址是   192.168.1.142



**第二步：找到你项目的地址路由**

如：我的本地javaweb项目地址是 127.0.0.1:8080

> [http://127.0.0.1:8080](http://127.0.0.1:8080)



**第三步：用Mac的内网ip地址替换掉127.0.0.1**

如：我的替换后是 

> [http://192.168.1.142:8080](http://192.168.1.142:8080)



那么，在同一个局域网下的  别人就可以访问你的本地项目了！







 版权声明：本文为博主原创文章，转载请标注： https://blog.csdn.net/hongyuancao/article/details/85758378

### 主要分为三个步骤：

**第一步：获取本Mac的ip地址**

可参考我的这篇文章：[Mac下查看本机IP地址](https://blog.csdn.net/hongyuancao/article/details/85758103)

如：我的ip地址是

> [192.168.3.94](http://192.168.3.94/basic/web/index.php?r=upload/test2)

**第二步：找到你项目的地址路由**

如：我的本地项目地址是

> [http://127.0.0.1/basic/web/index.php?r=xxx/test](http://127.0.0.1/basic/web/index.php?r=upload/test)

**第三步：把Mac的地址替换掉127.0.0.1**

如：我的替换后是 

> [http://192.168.3.94/basic/web/index.php?r=xxx/test2](http://192.168.3.94/basic/web/index.php?r=upload/test2)

那么，别人就可以访问你的本地项目了！

 

欢迎指导！