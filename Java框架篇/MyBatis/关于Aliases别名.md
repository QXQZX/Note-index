自定义类的别名:

在全局映射文件里 添加

```xml
<typeAliases>
  <!-- <typeAlias type="cn.coder.model.User" alias="_user"/> 单个设置 -->
  <!--指定包名  适用于包下所有的类   别名就是类名的第一个大写字母改成小写-->
  <package name="cn.coder.model"/>
</typeAliases>
```



其他默认别名

| 别名       | 映射的类型 |
| ---------- | ---------- |
| _byte      | byte       |
| _long      | long       |
| _short     | short      |
| _int       | int        |
| _integer   | int        |
| _double    | double     |
| _float     | float      |
| _boolean   | boolean    |
| string     | String     |
| byte       | Byte       |
| long       | Long       |
| short      | Short      |
| int        | Integer    |
| integer    | Integer    |
| double     | Double     |
| float      | Float      |
| boolean    | Boolean    |
| date       | Date       |
| decimal    | BigDecimal |
| bigdecimal | BigDecimal |





