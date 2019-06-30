### mappers

第一种：

<mapper resource=''/>

使用相对于类路径的资源

如：<mapper resource="sqlmap/User.xml" />

 

第二种：

<mapper url=''/> 【不用】

使用完全限定路径

如：<mapper url="file:///D:\workspace_spingmvc\mybatis_01\config\sqlmap\User.xml" />



第三种：

<mapper class=''/>

使用mapper接口的全限定名

如：<mapper class="cn.gyf.mybatis.mapper.UserMapper"/>

 

第四种：

 也可使用注解开发，把xml文件删除

**注意：此种方法要求mapper接口和mapper映射文件要名称相同，且放到同一个目录下**；



第五种：（推荐）

<package name=''/>（推荐）

**注册指定包下的所有映射文件**

如：<package name="cn.gyf.mybatis.mapper"/>

 **注意：此种方法要求mapper接口和mapper映射文件要名称相同，且放到同一个目录下**；

 

 