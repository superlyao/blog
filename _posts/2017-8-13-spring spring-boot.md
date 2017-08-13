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