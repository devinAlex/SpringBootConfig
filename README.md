# SpringBootConfig
## 一、自定义属性
  当我们创建一个springboot项目的时候，系统默认会为我们在src/main/java/resources目录下创建一个application.properties。application.properties
文件和application.yml文件，两种文件格式都支持。

在application.yml自定义一组属性，如果你需要读取配置文件的值只需要加@Value(“${属性名}”)。启动工程，访问：localhost:8080/miya,浏览器显示：forezp:12

## 二、将配置文件的属性赋给实体类
  有时候属性太多了，一个个绑定到属性字段上太累，官方提倡绑定一个对象的bean，这里我们建一个ConfigBean.java类，顶部需要使用注解
@ConfigurationProperties(prefix = “my”)来指明使用哪个。</br>

  application.yml：配置文件中${random} 可以用来生成各种不同类型的随机值，从而简化了代码生成的麻烦，例如 生成 int 值、long 值或者 string 字符串。</br>
  
  这里配置完还需要在spring Boot入口类加上@EnableConfigurationProperties并指明要加载哪个bean，如果不写ConfigBean.class，在bean类那边添加。</br>
  
  最后在Controller中引入ConfigBean使用即可。</br>
  
  ## 三、自定义配置文件
  上面介绍的是我们都把配置文件写到application.yml中。有时我们不愿意把配置都写到application配置文件中，这时需要我们自定义配置文件，比如test.properties:
  
  在最新版本的springboot，需要加这三个注解(User.java)。</br>
    @Configuration</br>
    @PropertySource(value = “classpath:test.properties”)</br>
    @ConfigurationProperties(prefix = “com.forezp”);</br>
   在1.4版本需要 PropertySource加上location。

## 四、多个环境配置文件

在现实的开发环境中，我们需要不同的配置环境；格式为application-{profile}.properties，其中{profile}对应你的环境标识，比如：</br>
application-test.properties：测试环境</br>
application-dev.properties：开发环境</br>
application-prod.properties：生产环境</br>
怎么使用？只需要我们在application.yml中加：</br>
```
spring:
  profiles:
    active: dev
```
其中application-dev.yml:
```
server:
  port: 8082
```
启动工程，发现程序的端口不再是8080,而是8082。
