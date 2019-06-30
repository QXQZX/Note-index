### JdbcTemplate插入中文乱码



**场景**：SpringBoot 使用jdbcTemplate插入数据，插入中文时，数据库为乱码。

**检测**：断点发现，浏览器提交到后台为中文，并未乱码；

 mysql字段编码格式为utf8;

**原因**：由于mysql装在阿里[云服务器](https://cloud.tencent.com/product/cvm?from=10680)中，远程连接时，配置如下：

```javascript
spring.datasource.url=jdbc:mysql://47.100.54.6/sz?useSSL=false&autoReconnect=true
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

并未配置此处连接的编码格式

**解决**：添加：characterEncoding=utf-8，修改为如下即可：

```javascript
spring.datasource.url=jdbc:mysql://47.100.54.6/sz?useSSL=false&characterEncoding=utf-8&autoReconnect=true
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```



转自：

https://cloud.tencent.com/developer/article/1386096