---
layout: post
title:  "spring boot入门"
date:   2017-8-1
categories: spring
tag: spring boot
---


* content
{:toc}

## 初始教程

### maven配置

```maven 
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.4.1.RELEASE</version>
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```
> 默认引入以下包
   
- spring-web, spring-webmvc Spring WebMvc框架
- tomcat-embed-* 内嵌Tomcat容器
- jackson 处理json数据
- spring-* Spring框架
- spring-boot-autoconfigure Spring Boot提供的自动配置功能

### 具体实现

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
 * Created by liaoyao on 2017/8/13.
 */
@Controller
@EnableAutoConfiguration
public class SpringBootTest {
    @RequestMapping("/test")
    @ResponseBody
    public String home() {
        return "spring boot";
    }

    public static void main(String[] arg) {
        SpringApplication.run(SpringBootTest.class, arg);
    }
}
```

- 它们都是由Spring Boot框架提供。在SpringApplication.run()方法执行后，Spring Boot的autoconfigure发现这是一个Web应用（根据类路径上的依赖确定），于是在内嵌的Tomcat容器中启动了一个Spring的应用上下文，并且监听默认的tcp端口8080（默认约定）。同时在Spring Context中根据默认的约定配置了Spring WebMvc：

* Servlet容器默认的Context路径是/
* DispatherServlet匹配的路径(servlet-mapping中的url-patterns)是/*
* @ComponentScan路径被默认设置为SampleController的同名package，也就是该package下的所有@Controller，@Service, * * * @Component, @Repository都会被实例化后并加入Spring Context中。

- 没有一行配置代码、也没有web.xml。基于Spring Boot的应用在大多数情况下都不需要我们去显式地声明各类配置，而是将最常用的默认配置作为约定，在不声明的情况下也能适应大多数的开发场景。