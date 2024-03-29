Spring Security
-
* add spring security dependency to project
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
```xml        
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-test</artifactId>
    <scope>test</scope>
</dependency>
```
* After adding dependencies go to any url , it will ask for login 
* in terminal a password will generate
* using username "root" and password you can login 
* it has login and logout page
* but we have to do the password comes from database
* all url is protected

![alt text](https://i.ibb.co/CJNjjN8/image.png)

* for development we have to enable all url 

* Create a new package `config`
* create a class inside this package named `SecurityConfig`, You can give any name
* add `@Configuration` annotatoin on this class

**@Bean**


create a dependency injection for `PasswordEncoder`

* inside `SecurityConfig` class, we will do dependency injection for `PasswordEncoder` interface

```java
@Autowired
    private PasswordEncoder passwordEncoder;
```
* when you run the file it will show error creating bean
* because of spring security is third party, spring ioc cannot know whom to dependency injection so we have to create a method of PasswordEncoder and apply @Bean annotation 
* to integrate third-party dependencies like Spring Security's PasswordEncoder, declare a method annotated with @Bean in a Spring configuration class for object creation.
* remove the dependency injection

create this method inside springboot configuration file 
```java
@Bean
    public PasswordEncoder getEncoder(){
        return new BCryptPasswordEncoder();
    }
```
we can use it inside runnable class( `UmsApplication.java` ) inside `com.ums` package

* @Bean annotation can only applied on methods, you cannot apply wherever you want

**Authorize http requests**
* inside SecurityConfig class create a method
```java
package com.ums.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.authorizeHttpRequests().anyRequest().permitAll();
        return http.build();
    }

}

```
* give the method name anything but the return type should be `SecurityFilterChain`
* HttpSecurity is a class comes from spring security and we need not to create the object for the class

![alt text](https://i.ibb.co/vLLzMPP/image.png)

add this line

>http.csrf().disable().cors().disable();

```java
@Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.csrf().disable().cors().disable();
        http.authorizeHttpRequests().anyRequest().permitAll();
        return http.build();
    }
```

* http.csrf().disable(): CSRF protection is a security measure that prevents attackers from exploiting the trust of authenticated users by tricking them into executing unauthorized actions. Disabling CSRF protection might be necessary in certain cases, such as when developing stateless APIs or when CSRF protection is handled by other means.

* http.cors().disable(): CORS is a security feature implemented by web browsers to restrict cross-origin HTTP requests initiated from scripts. Disabling CORS might be necessary when dealing with certain backend architectures or when handling cross-origin requests differently, such as using a reverse proxy or a different mechanism for controlling access.

**Encode password**
* make sure databse password length is more then 100
* USe this in service class
```java
AppUser maptoEntity(UserDto userDto){
        AppUser user = new AppUser();
        user.setName(userDto.getName());
        user.setUsername(userDto.getUsername());
        user.setEmail_id(userDto.getEmail_id());
        user.setPassword(new BCryptPasswordEncoder().encode(userDto.getPassword()));
        return user;
    }
```
Another way to encrypt password 

```java
AppUser maptoEntity(UserDto userDto){
        AppUser user = new AppUser();
        user.setName(userDto.getName());
        user.setUsername(userDto.getUsername());
        user.setEmail_id(userDto.getEmail_id());
        user.setPassword(BCrypt.hashpw(userDto.getPassword(), BCrypt.gensalt(10)));
        return user;
    }
```
