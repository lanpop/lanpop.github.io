---
layout: "post"
title: "spring-boot整合MyBatis"
date: "2019-03-06 10:10"
tag: [java,springboot,MyBatis]
expert: ""
---
---
layout: "post"
title: "springboot整合mybatis"
date: "2018-07-31 16:45"
---

pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>appb2</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>appb2</name>
	<description>Demo project for Spring Boot</description>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.3.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.apache.httpcomponents</groupId>
			<artifactId>httpclient</artifactId>
		</dependency>
		<!-- mybatis -->
		<dependency>
			<groupId>org.mybatis.spring.boot</groupId>
			<artifactId>mybatis-spring-boot-starter</artifactId>
			<version>2.0.0</version>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>
```

>mapper.java加注解`@Mapper`

```java
@Mapper
public interface SaveMapper {
	void saveUserinfo(Userinfo userinfo);
}
```
配置文件 application.properties，中添加数据源、MyBatis的实体和配置文件位置

```
server.port=58080

spring.datasource.url=jdbc:mysql://127.0.0.1:3306/lan
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.max-idle=10
spring.datasource.max-wait=10000
spring.datasource.min-idle=5
spring.datasource.initial-size=5

server.session.timeout=10
server.tomcat.uri-encoding=UTF-8


# mybatis.config= classpath:mybatis-config.xml
mybatis.mapperLocations=classpath:mappers/*.xml
# domain object's package
mybatis.typeAliasesPackage=com.lgp.SpringBoot.bean
# handler's package
# mybatis.typeHandlersPackage=
# check the mybatis configuration exists
# mybatis.check-config-location=
# mode of execution. Default is SIMPLE
# mybatis.executorType=
```
