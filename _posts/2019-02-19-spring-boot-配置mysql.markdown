---
layout: "post"
title: "spring boot 配置mysql"
date: "2019-02-19 00:27"
---

# 配置文件
```
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/lan?characterEncoding=utf-8&serverTimezone=GMT%2B8
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
```

>使用的mysql版本为：8.0.12  
driver，使用cj的，否则会有警告信息：`Loading class 'com.mysql.jdbc.Driver'. This is deprecated. The new driver class is 'com.mysql.cj.jdbc.Driver'. The driver is automatically registered via the SPI and manual loading of the driver class is generally unnecessary.`  
url后需添加serverTimezone=GMT%2B8，设置时区为东八区。  

# 数据库中中文显示 ？？
配置文件中数据库url中设置characterEncoding=utf-8

# 报错信息：java.sql.SQLException: Incorrect string value: '\xF0\x9F\x90\xBB' for column ...

修改配置文件my.ini
```
[client]
default-character-set=uft8
[mysqld]
character_set_server=uft8
collation-server=uft8_general_ci
```

重启数据库服务，查看表各列编码确认为utf8
![字符集]()
