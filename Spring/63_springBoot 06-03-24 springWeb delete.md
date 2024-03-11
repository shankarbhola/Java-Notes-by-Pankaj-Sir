
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
<!--updateregistration.jsp-->
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
* create a jsp page ```updateregistration.jsp```
* When you click on update button it will redirect to ```updateregistration.jsp``` page and Fetch all data by id before update
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ include file="menu.jsp" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Update</title>
</head>
<body>
	<h1>Update Registration</h1>
	<form action="updateReg" method="post">
		<pre>
			<input type="hidden" name="id" value="${registration.id}">
			First Name : <input type="text" name="firstName" value="${registration.firstName}">
			Last NAme : <input type="text" name="lastName" value="${registration.lastName}">
			Email : <input type="text" name="email" value="${registration.email}">
			Mobile : <input type="text" name="mobile" value="${registration.mobile}">
			<input type="submit" value="Update">
		</pre>
	</form>
</body>
</html>
```
```java
//controller
@RequestMapping("/get-by-id")
	public String getRegistrationById(@RequestParam("id") long id, Model model) {
		Registration registration = registrationService.getRegistrationById(id);
		model.addAttribute("registration",registration);
		return "updateregistration";
	}
```
```java
//service
@Override
	public Registration getRegistrationById(long id) {
		Optional<Registration> byId = registrationRepository.findById(id);
		Registration registration = byId.get();
		return registration;
	}
```

* it will show all the data of a record of the id in input field 
* change data and click on update button
* after clicking update button it will go to ```/updateReg``` page which is managed by controller
```java
//controller
@RequestMapping("/updateReg")
	public String updateRegistration(RegistrationDto dto, Model model) {
		Registration registration = new Registration();
		
		registration.setId(dto.getId());
		registration.setFirstName(dto.getFirstName());
		registration.setLastName(dto.getLastName());
		registration.setEmail(dto.getEmail());
		registration.setMobile(dto.getMobile());
		
		registrationService.updateRegistration(registration);
		
		List<Registration> registrations = registrationService.findAllRegistrations();
		model.addAttribute("registrations",registrations);
		return "listregistrations";
		
	}
```
* using dto send the values to entity class
* call the service layer and supply the Registration object
```java
//service
@Override
	public void updateRegistration(Registration registration) {
		registrationRepository.save(registration);
	}
```
* in service layer,  call the repository layer and pass the value
* repository layer update the record
