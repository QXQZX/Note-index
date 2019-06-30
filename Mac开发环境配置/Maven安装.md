### Maven安装

学习接触Java框架必不可少的东西  maven



安装配置：

1. 首先配置好Java的SDK  的环境变量

```bash
$ vi .bash_profile  # 使用zsh的小伙伴 vi .zshrc

# 添加如下 环境变量
export PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_212.jdk/Contents/Home
# 注意 jdk版本可能不一记得修改
```

	2. 之后检查是否配置完成

```bash
# 执行
$ java -version

######显示如下内容则证明配置成功######
java version "1.8.0_212"
Java(TM) SE Runtime Environment (build 1.8.0_212-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.212-b12, mixed mode)
```



	3. Maven  安装(利用mac强大的包Homebrew管理器)

```bash
$ brew search maven
$ brew info maven
$ brew install maven
```

	4. 配置maven环境变量

```bash
$ vi .bash_profile  # 使用zsh的小伙伴 vi .zshrc

# 添加如下 环境变量
# Maven
export M2_HOME=/usr/local/Cellar/maven/3.6.1/libexec
export PATH=$PATH:$M2_HOME/bin
# 注意 maven版本可能不一记得修改
```

	5. 检查是否配置成功

```bash
$ mvn -version

######显示如下内容则证明配置成功######
Apache Maven 3.6.1 (d66c9c0b3152b2e69ee9bac180bb8fcc8e6af555; 2019-04-05T03:00:29+08:00)
Maven home: /usr/local/Cellar/maven/3.6.1/libexec
Java version: 1.8.0_212, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_212.jdk/Contents/Home/jre
Default locale: zh_CN, platform encoding: UTF-8
OS name: "mac os x", version: "10.14.5", arch: "x86_64", family: "mac"
```

