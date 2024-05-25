* Create an JSP file inside views named ```list_registration.jsp```
* call it using controller
```java
//RegistrationController.jsp
@RequestMapping("/list-all")
	public String listRegistration() {
		return "list_registration";
	}
```
* Add JSTL library to pom.xml
* Add JSTL [core tag library](https://www.tutorialspoint.com/jsp/jsp_standard_tag_library.htm) to jsp page
* JSTL core tag libraryhelps to convert JSTL to java code
```jap
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core" %>
```
```jsp
//list_registration.jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>List Registration</title>
</head>
<body>
	<h2>JSTL tags...</h2>
	<c:out value="Hello"></c:out>
	
	<c:set var="x" value="10000"></c:set>
	<c:out value="${x}"/>
	
	<c:if test = "${x > 2000}">
         <p>My salary is:  <c:out value = "${x}"/><p>
      </c:if>
      
     <c:forEach var = "i" begin = "1" end = "5">
         Item <c:out value = "${i}"/><p>
      </c:forEach>
</body>
</html>
```

**Display all registration records on ```list_registration.jsp```**
* create a method on service layer
```java
//RegistrationService.java
package com.webapp.service;

import java.util.List;

import com.webapp.entity.Registration;

public interface RegistrationService {
	public void addRegistration(Registration registration);

	public List<Registration> findAllRegistrations();
}
```
```java
//RegistrationServiceImpl.java
package com.webapp.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.webapp.entity.Registration;
import com.webapp.repository.RegistrationRepository;

@Service
public class RegistrationServiceImpl implements RegistrationService {

	@Autowired
	private RegistrationRepository rep;
	
	@Override
	public void addRegistration(Registration registration) {
		rep.save(registration);
	}

	@Override
	public List<Registration> findAllRegistrations() {
		List<Registration> registrations = rep.findAll();
		return registrations;
	}

}
```
* Call view and service layer from Controller layer
```java
//RegistrationController.java
@RequestMapping("/list-all")
	public String listRegistration(Model model) {
		List<Registration> registrations = res.findAllRegistrations();
		model.addAttribute("registrations", registrations);
		return "list_registration";
	}
```