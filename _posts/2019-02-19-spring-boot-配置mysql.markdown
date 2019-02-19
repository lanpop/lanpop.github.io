---
layout: "post"
title: "spring boot 配置mysql"
date: "2019-02-19 00:27"
---

配置文件
```
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/lan?serverTimeZone=GMT%2B8"
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
```

>使用的mysql版本为：8.0.12  
driver，使用cj的，否则会有警告信息：`Loading class 'com.mysql.jdbc.Driver'. This is deprecated. The new driver class is 'com.mysql.cj.jdbc.Driver'. The driver is automatically registered via the SPI and manual loading of the driver class is generally unnecessary.`  
url后需添加serverTimeZone=GMT%2B8，设置时区为东八区。  
