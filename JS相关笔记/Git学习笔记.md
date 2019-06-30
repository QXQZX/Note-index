## Git

#### 1.什么是git

git是一种版本管理的工具(VCS)    它在开发的过程中具有以下的几个特点：

* 分布式版本控制
* 多个工作人员协调工作
* 有效监听谁做的修改
* 本地及远程操作

#### 2.git的基础命令行操作

```bash
$ git init // 初始化本地git仓库
$ git add <file> // 添加文件
$ git status  // 查看状态
$ git commit -m "" // 提交
$ git push    // 推送到仓库
$ git pull    // 从远程仓库拉取数据
$ git clone   // 从远程拷贝数据
```

```bash
$ git add <file>  //添加后  可以用以下的命令
		$ git add *.html  // 添加所有以HTML结尾的文件
		$ git add .       // 添加所有的文件
$ git status    // 查看添加状态
$ git rm --cached <filename>  // 删除已经添加在队列中的文件

```

#### 3.git的使用

##### <1>使用git  忽略一下不想上传的文件

```bash
$ touch .gitignore  // 创建忽略配置文件
/*关于gitignore的编写规则  查看官方文档*/
$ 
```

#####<2> 主线及分支的使用(重要)

```bash
$ git branch <branchname>     /*创建分支*/
$ git checkout <branchname>   /*切换分支*/
/*先git clone下整个仓库  再用  git checkout xxxx  切换分支查看不同分支的代码*/
```

主线(master)和分支的conmmit互不干扰

```bash
$ git merge xxx   //  会将xxx和当前所在的分支合并
```

#####<4> 操作远程仓库

```bash
$ git remote //  查看远端
$ git romote add origin https://github.com/xxx/xxx.git  // 添加远端
$ git push -u origin master  // push到远端的仓库
```

<5> 基础的流程

```ke&#39;lon
1. 在github官网创建账号
2. 创建远程仓库
3. 克隆仓库
4. 在本地仓库储存数据
5. 提交数据并备注信息
6. 同步本地数据到远程仓库
```



