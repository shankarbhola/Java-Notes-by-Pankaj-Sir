```jsp
<!--list_registration.jsp-->
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ include file="menu.jsp" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>List Registration</title>
</head>
<body>
	<h2>JSTL tags...</h2>
	<table>
		<tr>
			<td>First Name</td>
			<td>Last Name</td>
			<td>Email</td>
			<td>Mobile</td>
		</tr>

		<c:forEach items="${registrations}" var="registration">
			<tr>
				<td>${registration.firstName}</td>
				<td>${registration.lastName}</td>
				<td>${registration.email}</td>
				<td>${registration.mobile}</td>
			</tr>
		</c:forEach>
	</table>
</body>
</html>
```

* create a menu.jsp file and inclue it on all pages
```jsp
<!-- menu.jsp -->
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
</head>
<body>
	<a href="list-all">All Registrations</a>
	<a href="view-reg-page">New Registration</a>
</body>
</html>
```
Delete Record
-

* add delete button on every row
```jsp
<!--list_registration.jsp-->
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
		</tr>
	
	<c:forEach items="${registrations}" var="registration">
		<tr>
			<td>${registration.firstName}</td>
			<td>${registration.lastName}</td>
			<td>${registration.email}</td>
			<td>${registration.mobile}</td>
			<td><a href="delete?id=${registration.id}">Delete</a></td>
		</tr>
	</c:forEach>
	</table>
</body>
</html>
```

* go to controller create a delete method and check the id comes to backend or not
```java
//RegistrationController.java
@RequestMapping("/delete")
	public String deleteRegistration(@RequestParam("id") long id) {
		System.out.println(id);
		return null;
	}
```