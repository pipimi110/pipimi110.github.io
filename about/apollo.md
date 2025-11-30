apollo
服务端#quick start#linux启动

```
wsl有网络问题，需要添加各种参数配置wsl ip；开发客户端的idea访问不通localhost(wsl)

java -jar   -Deureka.instance.hostname=172.25.179.206   -Deureka.instance.ip-address=172.25.179.206   -Dspring.cloud.inetutils.preferred-networks=172.25.179.206   -Dapollo.configService.ip=172.25.179.206   -Dserver.address=0.0.0.0   apollo-all-in-one.jar
```

客户端
https://www.apolloconfig.com/#/zh/design/apollo-introduction?id=_4%e3%80%81apollo-in-depth
客户端java
```
Config config = ConfigService.getAppConfig();
Integer defaultRequestTimeout = 200;
Integer requestTimeout = config.getIntProperty("requestTimeout", defaultRequestTimeout);
```

客户端spring-boot#windows
```
Apollo和Spring也可以很方便地集成，只需要标注@EnableApolloConfig后就可以通过@Value获取配置信息：

@Configuration
@EnableApolloConfig
public class AppConfig {}

@Component
public class SomeBean {
    //timeout的值会自动更新
    @Value("${request.timeout:200}")
    private int timeout;
}
```

https://github.com/apolloconfig/apollo-use-cases/blob/master/spring-boot-logger/src/main/java/com/ctrip/framework/apollo/use/cases/spring/boot/logger/Application.java
```
<dependency>
        <groupId>com.ctrip.framework.apollo</groupId>
        <artifactId>apollo-client</artifactId>
        <version>2.4.0</version>
    </dependency>

application.properties
app.id=spring-boot-logger
# set apollo meta server address, adjust to actual address if necessary
apollo.meta=http://localhost:8080
```
```
package com.example.demo;

import com.ctrip.framework.apollo.spring.annotation.EnableApolloConfig;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.web.servlet.ServletComponentScan;

@ServletComponentScan(basePackages="com.example.demo")
@SpringBootApplication
@EnableApolloConfig //EnableApolloConfig注解
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}

```
