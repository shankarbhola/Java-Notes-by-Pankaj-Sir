* Go to src/main > right click > new > foler
* create folder  ```webapp/WEB-INF/views``` inside ```src/main``` folder like ```src/main/webapp/WEB-INF/views```

* right click on views create a JSP page
* create ```registration.jsp``` file inside ```src/main/webapp/WEB-INF/views/```
* inside WEB-INF , files cannot be direct access
* it can called only by controller

**How to create controller layer**
* To create a controller layer create a package named ```com.webapp.controller``` inside ```src/main/java/```
* Create a class ```RegistrationController.java``` inside ```src/main/java/com.webapp.controller```
* This is an ordinary java class 
* to make this controller layer apply the annotation ```@Controller```

```java
//RegistrationController.java
package com.webapp.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class RegistrationController {
	//handler methods
	//http://localhost:8080/view-registration-page
	@RequestMapping("/view-registration-page")
	public String viewRegistrationpage() {
	return "registration"; 	
	}
}
```
Here return acts as request dispatcher
* Spring web follows MVC architecture
* for path, we have to add prefix and suffix inside ```application.properties``` file

```properties
//application.properties
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```
* if we run this file it will show error due to spring jpa dependency
* so we have to add connection to the database
```properties
//application.properties

spring.datasource.url=jdbc:mysql://localhost:3306/web_app_db
spring.datasource.username=root
spring.datasource.password=system

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```
* if it showing same error, just remove db name and again type db name then save the file
* If we run the file it will show 404 error 
* to overcome this error we have to add tomcat dependency
* go to google & search ```jasper tomcat for jsp spring boot```
* open stackoverflow website & copy tomcat dependency 
```xml
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
    <scope>provided</scope>
</dependency>
```
* add this dependency to ```pom.xml``` file
* Run the project in spring boot app
* open browser and go to ```http://localhost:8080/view-registration-page``` it will load the jsp file

Create entity layer
```java
package com.webapp;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name="registrations")
public class Registration {
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private int id;
	
	@Column(name = "first_name" , nullable = false , length = 20)
	private String firstName;
	
	@Column(name = "last_name" , nullable = false , length = 20)
	private String lastName;
	
	@Column(name = "email" , nullable = false , length = 128 , unique = true)
	private String email;
	
	@Column(name = "mobile" , nullable = false , length = 10)
	private String mobile;

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getFirstName() {
		return firstName;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getLastName() {
		return lastName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}

	public String getMobile() {
		return mobile;
	}

	public void setMobile(String mobile) {
		this.mobile = mobile;
	}
	
	
}
```