Send welcome email after registration
-
* go to mail.google.com
* click on Google apps which is left side of profile icon
* click on account
* On the search bar Search ```2-Step``` and Turn on 2-Step Verification
* On the search bar Search ```app passwords```, you will only get this after step-2 verification enable
* Give a app name and create
* You will get a password
* copy the email and password and paste it on notepad
* add mail dependency on pom.xml file
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```
* go to application.properties file and set email details
```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=your-email@gmail.com
spring.mail.password=your-gmail-password
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
spring.mail.properties.mail.smtp.starttls.required=true
```
* create a package named ```com.webapp.util```
* inside this package create a class named ```EmailService```
```java
package com.webapp.util;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.mail.SimpleMailMessage;
import org.springframework.mail.javamail.JavaMailSender;

public class EmailService {
	
	@Autowired
	private JavaMailSender javaMailSender;
	public void sendEmail(String to, String sub, String msg) {
		SimpleMailMessage sm = new SimpleMailMessage();
		sm.setTo(to);
		sm.setSubject(sub);
		sm.setText(msg);
		javaMailSender.send(sm);
	}
}
```
* go to controller and create object of ```EmailService``` class
```java
//controller
@Autowired
	private EmailService emailService;
```
* if we run the application it will show error
>Error creating bean

* EmailService class is an ordinary java class
* in spring boot to create its object you can either apply @Service or @Coponent
* it will handover the java class to spring Boot and now spring IOC can create object of the class
* as we write businesslogic and database operation in service layer, this is utility layer for sending email so we make it as @Component
```java
//EmailService.java
package com.webapp.util;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.mail.SimpleMailMessage;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.stereotype.Component;

@Component
public class EmailService {
	
	@Autowired
	private JavaMailSender javaMailSender;
	public void sendEmail(String to, String sub, String msg) {
		SimpleMailMessage sm = new SimpleMailMessage();
		sm.setTo(to);
		sm.setSubject(sub);
		sm.setText(msg);
		javaMailSender.send(sm);
	}
}
```
* send the mail after new registration

* you can @ModelAttribute or can use dto
```java
//using @ModelAttribute
//controller
@RequestMapping("/saveReg")
	public String saveRegistration(@ModelAttribute Registration registration) {
		registrationService.addRegistration(registration);
		emailService.sendEmail(registration.getEmail(), "Test", "Hello");
		return "registration";
	}
```
```java
//using dto
//controller
@RequestMapping("/saveReg")
	public String addRegistration(RegistrationDto dto) {
		Registration registration = new Registration();
		registration.setFirstName(dto.getFirstName());
		registration.setLastName(dto.getLastName());
		registration.setEmail(dto.getEmail());
		registration.setMobile(dto.getMobile());
		res.addRegistration(registration);
		emailService.sendEmail(dto.getEmail(), "Hello", "Hiii");
		return "registration";
	}
```

