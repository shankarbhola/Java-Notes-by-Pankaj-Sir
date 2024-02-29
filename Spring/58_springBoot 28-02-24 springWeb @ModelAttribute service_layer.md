create a form in jsp file
```jsp
<!--registration.jsp-->
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Registration</title>
</head>
<body>
	<h1>Add Registration</h1>
	<form action="saveReg" method="post">
		<pre>
			First Name : <input type="text" name="firstName">
			Last NAme : <input type="text" name="lastName">
			Email : <input type="text" name="email">
			Mobile : <input type="text" name="mobile">
			<input type="submit" value="Save">
		</pre>
	</form>
</body>
</html>
```
**Create a repository layer**
```java
//RegistrationRepository.java
package com.webapp.repository;
import org.springframework.data.jpa.repository.JpaRepository;
import com.webapp.entity.Registration;

public interface RegistrationRepository extends JpaRepository<Registration, Long> {

}
```
Take data from views to controller layer
```java
//RegistrationController.java
package com.webapp.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;

import com.webapp.entity.Registration;
import com.webapp.service.RegistrationService;

@Controller
public class RegistrationController {
	
	@Autowired
	private RegistrationService registrationService;
	
	@RequestMapping("/view-reg-page")
	public String viewRegistrationPage() {
		return "registration";
	}
	
	@RequestMapping("/saveReg")
	public String saveRegistration(@ModelAttribute Registration registration) {
		registrationService.addRegistration(registration);
		return "registration";
	}
}
```
* @ModelAttribute in Spring MVC helps in binding data from the view to a model attribute, typically a Java object. When a form is submitted, the form fields' values are automatically mapped to the corresponding fields of the model attribute class.

**create a service layer**
* inside ```src/main/java``` create a package named ```com.webapp.service```
* inside ```src/main/java/com.webapp.service``` create an interface 
```java
//RegistrationService.java
package com.webapp.service;

import com.webapp.entity.Registration;

public interface RegistrationService {
	public void addRegistration(Registration  registration);
}
```
* inside ```src/main/java/com.webapp.service``` create an class
```java
//RegistrationServiceImpl.java
package com.webapp.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.webapp.entity.Registration;
import com.webapp.repository.RegistrationRepository;

@Service
public class RegistrationServiceImpl implements RegistrationService {
	
	@Autowired
	private RegistrationRepository registrationRepository;
	
	@Override
	public void addRegistration(Registration registration) {
		registrationRepository.save(registration);
	}

}
```