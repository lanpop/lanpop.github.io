---
layout: "post"
title: "SpringMVC学习笔记"
date: "2018-12-11 16:07"
---

# 搭建SpringMVC项目的步骤：
1. 初始化SpringMVC的DispatcherServlet；
2. 搭建转码过滤器，保证客户端请求进行正确的转码；
3. 搭建视图解析器（view resolver），告诉Spring去哪里查找视图，以及它们是使用哪种方言编写的（JSP、Thymeleaf模版等）；
4. 配置静态资源的位置（CSS、JS）；
5. 配置所支持的地域以及资源bundle；
6. 配置multipart解析器，保证文件上传能够正常工作；
7. 将Tomcat或Jetty包含进来，从而能够在Web服务器上运行我们的应用；
8. 建立错误页面（如404）。

# 分发器和multipart配置

`DispatcherServletAutoConfiguration`是一个典型的Spring Boot配置类。  
* 与其他Spring配置类相同，使用了@Configuration注解；
* 一般会通过@Order（`@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)`）注解来生命优先等级，可以看到DispatcherServletAutoConfiguration需要优先进行配置;
* 其中也可以包含一些提示信息，如`@AutoConfigureAfter(ServletWebServerFactoryAutoConfiguration.class)`或@AutoconfigureBefore，从而进一步细化配置处理的顺序；
* 它还支持在特定的条件下启用某项功能。通过使用`@ConditionalOnClass(DispatcherServlet.class)`这个特殊的配置，能够保证我们的类路径下包含DispatcherServlet，这能够很好地表明Spring MVC位于类路径中，用户当前希望将其启动起来。
