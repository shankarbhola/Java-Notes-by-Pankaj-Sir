Check Whether user exists or not & return boolean value

```java
//EmployeeRepository.java
boolean existsByEmail(String email);
boolean existsByName(String name);
```
```java
//Test
@Test
void checkUserExistByEmail() {
    boolean val = employeeRepository.existsByEmail("mike@gmail.com");
    System.out.println(val);
}
	
@Test
void checkUserExistByName() {
    boolean val = employeeRepository.existsByName("mike");
    System.out.println(val);
}
```

##Spring Web project##

By default web tool not installed in spring 
* go to help > eclipse market place
* search jsp
* install "Eclipse Enterprise Java and Web Developers Tools 3.31"

![](https://i.ibb.co/BLZLz6f/image.png) 

* Go to src/main > right click > new > foler
* create folder  ```webapp/WEB-INF/views``` inside ```src/main``` folder like ```src/main/webapp/WEB-INF/views```

* right click on views create a JSP page
* Create a controller layer ```src/main/java/com.webapp.controller```
* Create a class inside this package called ```RegistrationController.java```
* This is an ordinary java class 
* to make this controller layer apply the annotation ```@Controller```

```java
//RegistrationController.java
package com.webapp.controller;
import org.springframework.stereotype.Controller;

@Controller
public class RegistrationController {
	//handler methods
}
```