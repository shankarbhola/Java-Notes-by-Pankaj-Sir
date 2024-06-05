Debug this project

https://github.com/Amit8127/Book-My-Show.git



## Swagger implementation in Spring Boot ##

* Add validation dependency for generate validations with Swagger

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
* add spring doc openapi dependency

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.5.0</version>
</dependency>
```

Use url to access Swagger Ui [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)