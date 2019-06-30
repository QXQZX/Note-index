## BaiduPCS-Go简介

BaiduPCS-Go是一个用Go语言编的命令行版的百度网盘，我们可以类比mac和Appstore的关系。那么为什么要用这样一个安装比较麻烦，还要记命令行的百度网盘的替代品，直接用百度网盘客户端不好么？

<!--more-->

这还真的是不好，百度网盘在mac下是一个十足的阉割版，最常用的功能中，Mac版缺失了以下几种功能：

- **没有分享功能**：mac下的客户端的分享功能居然是需要通过浏览器打开，太不优雅了。
- **没有离线下载任务：**直接导致不能下载磁力链接。

如果你和我一样平时一样习惯终端操作，这个工具的学习成本超级低，同时它还有一定的**提升下载速度**的功效。

所以今天主要介绍mac下的BaiduPCS-Go使用说明。

开源地址：https://github.com/iikira/BaiduPCS-Go

-------------

### BaiduPCS-Go mac安装指南

#### 安装

Mac一般是预装了go的。

**如果没有go的话**，使用以下命令来安装。

```bash
brew install go
```

除了go我们还需要安装git，**如果没有的话**同样使用

```bash
brew install git
```

再**如果你没有的brew**的话，没事问题不大，安装就完事了

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

在拥有了git和go以后，执行下面的指令即可安装BaiduPCS-Go了。

```bash
go get -u -v github.com/iikira/BaiduPCS-Go
```

#### 配置环境文件

之后根据安装时的提示，一般将会安装在~/go/bin目录下，之后需要**手动添加到环境变量**中，分以下两种情况。

注：修改zshrc和bashrc文件，需要重启终端后才能生效
使用Oh my zsh的用户,在~/.zshrc最后一行中添加如下指令,   **将其中qxqzx换为自己的用户名**

```bash
export PATH="/Users/deamov/go/bin:$PATH"
```



#### 使用：

关于BaiduPCS-Go常用操作第一次使用需要有登陆的操作，输入login即可登陆，尊许提示依次输入账户和密码即可，如果需要验证码，则会输出一个链接，打开就可以看到验证码了。
2、BaiduPCS-Go基本操作
1）、基本的移动目录的方式和linux的操作一样，ls是现实当前目录的文件，rm是删除命令，cd是切换目录，创建目录是mkdir，拷贝是cp，值得一提的是它支持Tab补全。和平时使用的终端命令不同的有如下几个指令。

2）、下载：记住是download就好啦
download <网盘文件或目录的路径1> 
d <网盘文件或目录的路径1> <文件或目录2> <文件或目录3> ...



效果：

![](https://tuku.jdblog.cn/2019/05/24/c246b274-9a0b-4205-a729-4847106bb64d.png)



这个工具很强大，还可以通过设置下载线程数等等操作来提升下载速度，更多详细的操作请参考它的官网。

更多使用 去github自己看使用说明吧