springmvc和json整合配置方法



### 配置方法一

1、导入第三方的jackson包，

jackson-mapper-asl-1.9.7.jar

和jackson-core-asl-1.9.7.jar。 

2、[spring](http://lib.csdn.net/base/17)配置文件添加**



```xml
<mvc:annotation-driven/>

<!-- 避免IE执行AJAX时,返回JSON出现下载文件 -->  
<bean id="mappingJacksonHttpMessageConverter" class="org.springframework.http.converter.json.MappingJacksonHttpMessageConverter">  
  <property name="supportedMediaTypes">  
    <list>  
      <value>text/html;charset=UTF-8</value>  
    </list>  
  </property>  
</bean>  

<!-- 启动Spring MVC的注解功能，完成请求和注解POJO的映射 -->  
<bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter">  
  <property name="messageConverters">  
    <list>  
      <ref bean="mappingJacksonHttpMessageConverter" /><!-- json转换器 -->  
    </list>  
  </property>  
</bean> 
```





### 配置方案二(常用)

1、导入第三方的fastjson包，

fastjson-1.1.34.jar 

2、Spring配置文件添加：

```xml
<mvc:annotation-driven>
  <mvc:message-converters register-defaults="true">
    <!-- 避免IE执行AJAX时,返回JSON出现下载文件 -->
    <bean id="fastJsonHttpMessageConverter" class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
      <property name="supportedMediaTypes">
        <list>
          <value>application/json;charset=UTF-8</value>
        </list>
      </property>
    </bean>
  </mvc:message-converters>
</mvc:annotation-driven>
```





### 配置方案三

1、需要导入 

jackson-annotations-*.jar,

jackson-core-*.jar,

jackson-databind-*.jar 

2、在spring中添加配置



```xml
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping" />
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">
  <property name="messageConverters">
    <list>
      <bean class="org.springframework.http.converter.StringHttpMessageConverter">
        <property name="supportedMediaTypes">
          <list>
            <value>text/html; charset=UTF-8</value>
            <value>application/json;charset=UTF-8</value>
          </list>
        </property>
      </bean>
      <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
        <property name="supportedMediaTypes">
          <list>
            <value>text/html; charset=UTF-8</value>
            <value>application/json;charset=UTF-8</value>
          </list>
        </property>
      </bean>
    </list>
  </property>
</bean>
```

 