* **If we create a JSP page in webapp , this page can directly access without login**
* **To overcome this proble we have to create JSP page inside WEB-INF folder**
* **Only a servlet can run this file**
**View**
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>New Registration</h1>
	<form action="newRegistration" method="post"> <br>
		Name: <input type="text" name="name"/> <br>
		Course: <input type="text" name="course"/> <br>
		Email: <input type="text" name="email"/> <br>
		Mobile: <input type="text" name="mobile"/> <br>
		<input type="submit" value="Save">
	</form>
	<a href="updateRegistration">Update Registration</a>
	<a href="retriveRegistration">View All Registration</a> <br>
	<a href="deleteRegistration">Delete Registration</a> <br>
</body>
</html>
```
**Controller**
```java
package com.registration.controller;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.registration.model.DAOserviceImpl;


@WebServlet("/newRegistration")
public class NewRegistrationController extends HttpServlet {
	private static final long serialVersionUID = 1L;

    public NewRegistrationController() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String name = request.getParameter("name");
		String course = request.getParameter("course");
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		
		DAOserviceImpl service = new DAOserviceImpl();
		service.connectDB();
		int newreg = service.createRegistration(name, course, email, mobile);
		
		PrintWriter out = response.getWriter();

		if (newreg!=0) {
			out.print("<script>alert('Record created successfully');setTimeout(function() { window.history.back(); }, 0);</script>");
		} else {
			out.print("<script>alert('Failed to create record');setTimeout(function() { window.history.back(); }, 0);</script>");
		}
	}

}

```
**Model**
```java
@Override
	public int createRegistration(String name, String course, String email, String mobile) {
		try {
			int newreg = stmnt.executeUpdate("insert into registration values('"+name+"','"+course+"','"+email+"','"+mobile+"')");
			return newreg;
		} catch (Exception e) {
			e.printStackTrace();
		}
		return 0;
	}
```