# 使用gitee搭建免费的图床

没有微博的免费图床之后的我开始想你们搞一个免费的图床。

想到之前自己在GitHub上搭建过一个GitHub Page的图床，勉强能用，但是访问速度很慢，不得不因此弃用。于是就想到了Gitee（码云），这个可不可以搭建一个免费的page服务，托管我的图片呢？使用gitee搭建的图床，可以防止图片数据的丢失（只要码云不死）。

一查Gitee官网真有，于是二话不说，开干！

<!--more-->



### 一、准备工作

1、首先要有一个gitee帐户

2、然后在本地配置一下自己的SSH

3、最后本地有Git环境，用于后面图片的提交

准备工作这三步，就不具体展开了，没有环境的动起手来，先把环境搭好。要熟悉使用push 和 clone



### 二、开始干活

#### 1、创建一个项目

 点击 `+`新建一个项目，填写项目名称，点击下面的 `创建`，如下图：

![新建项目](https://iqxqzx.gitee.io/pic/images/2019/7/25/01.png)

![img](https://dufyun.gitee.io/images_bed/images/techy/Snipaste_2018-11-23_22-30-06.png)

#### 2、添加文件 index.html(名称必须是index.html)

![添加index.html](https://iqxqzx.gitee.io/pic/images/2019/7/25/02.png)

![index.html](https://dufyun.gitee.io/images_bed/images/techy/Snipaste_2018-11-23_22-35-05.png)

#### 3、选择 pages 服务并启动

![选择page服务并启动](https://iqxqzx.gitee.io/pic/images/2019/7/25/03.png)



#### 4、访问生成的网站地址

已开启 Gitee Pages 服务后，访问page首页地址，这个是我的首页：https://iqxqzx.gitee.io/pic

**到此一个gitee page 已经搭建哦克 了！** 真正让图床起作用请继续往下看！



#### 5、将gitee图床项目拉取到本地

 这一步不做介绍，就是将gitee上刚才创建的项目拉取到本地。



#### 6、优化 gitee page 首页

因为我只是用来保存图片，所以就没有在集成博客系统。如果你需要你可以将此page 和 hexo等博客系统集成。

我这里只是为了首页好看，去模板之家找一套模板！ 

然后自己修改了一下，删除不需要的文件，然后就直接放到 第五步 下载的 项目路径，**commit、push！**

![本地目录](https://iqxqzx.gitee.io/pic/images/2019/7/25/04.png)

然后就可以访问感觉比较舒服的首页了！访问地址：https://iqxqzx.gitee.io/pic



#### 7、关于图片的存放

把图片传到images目录下，或者其他自定义目录，commit  &  push 之后到服务->giteePages->  重新部署网站。

而后就可以直接按照目录提取图片了

例如：

```
https://iqxqzx.gitee.io/pic/images/2019/7/22/python_cuda_04.png
```



### 三、简单总结

看似整个过程很简单，但是还是建议想要一个免费的图床，自己有没有专门图片服务器的伙伴动手搞一下，小的积累，带来大个改变！

如果图床是公开的，建议不要上传比较隐私的图片，以及上传合法的图片！



### 四、备注说明

本篇博文的图片就是来自我gitee搭建的图床！**右键 --> 在新标签页打开图片** ，即可看到我图床的地址！

