
```java
//RegistrationController.java
@RequestMapping("/delete")
	public String deleteRegistration(@RequestParam("id") long id, ModelMap model) {
		registrationService.deleteRegistration(id);
		List<Registration> registrations = registrationService.findAllRegistrations();
		model.addAttribute("registrations",registrations);
		return "listregistrations";
	}
```
* for add attribute ue can use Model or ModelMap
```java
//RegistrationServiceImpl.java
@Override
	public void deleteRegistration(long id) {
		registrationRepository.deleteById(id);
	}
```
Update Record
-
* Get all the id values 
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ include file="menu.jsp" %>
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>List Registration</title>
</head>
<body>
	<h1>All Registration...</h1>

	<table>
		<tr>
			<th>First Name</th>
			<th>Last Name</th>
			<th>Email</th>
			<th>Mobile</th> 
			<th>Delete</th>
			<th>Update</th>  
		</tr>
	
	<c:forEach items="${registrations}" var="registration">
		<tr>
			<td>${registration.firstName}</td>
			<td>${registration.lastName}</td>
			<td>${registration.email}</td>
			<td>${registration.mobile}</td>
			<td><a href="delete?id=${registration.id}">Delete</a></td>
			<td><a href="get-by-id?id=${registration.id}">Update</a></td>
		</tr>
	</c:forEach>
	</table>
</body>
</html>
```