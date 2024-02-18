## MVC Mini Project ##
![picture](https://i.ibb.co/rFtbNw1/VID-20240208-145303.gif)
![picture](https://i.ibb.co/7WfKkwP/image.png)
### Login ###
**View**
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Login</title>
</head>
<body>
	<form action="loginvalidate" method="post">
		Email : <input type="text" name="email"/> <br>
		Password : <input type="password" name="password"/> <br>
		<input type="submit"/>
	</form>
	<%
	if(request.getAttribute("msg")!=null){
		out.print(request.getAttribute("msg"));
	}
	%>
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

import com.registration.module.DAOserviceIMPL;



@WebServlet("/loginvalidate")
public class LoginValidateController extends HttpServlet {
	private static final long serialVersionUID = 1L;
     
    public LoginValidateController() {
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String email = request.getParameter("email");
		String password = request.getParameter("password");
		
		DAOserviceIMPL service = new DAOserviceIMPL();
		service.connectDB();
		boolean verifyLogin = service.verifyLogin(email, password);
		if (verifyLogin) {
			RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/NewRegistration.jsp");
			rd.forward(request, response);
		} else {
			request.setAttribute("msg", "Invalid Id or Password");
			RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
			rd.forward(request, response);
		}
	}

}

```
**Model**
```java
package com.registration.module;

import java.sql.ResultSet;

public interface DAOservice {
	public void connectDB();
	public boolean verifyLogin(String email, String password);
	public void createRegistration(String name, String course, String email, String mobile);
	public void deleteRegistration(String email);
	public void updateRegistration(String email, String mobile);
	public ResultSet retriveRegistration();
}
```
```java
package com.registration.module;

import java.sql.*;
public class DAOserviceIMPL implements DAOservice {
	Connection con;
	Statement stmnt;
	@Override
	public void connectDB() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_reg_db","root","system");
			stmnt = con.createStatement();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

	@Override
	public boolean verifyLogin(String email, String password) {
		try {
			ResultSet result = stmnt.executeQuery("select * from login where email='"+email+"' and password='"+password+"'");
			if (result.next()) {
				return true;
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
		return false;
	}

}

```
* If we create a JSP page in webapp , this page can directly access without login
* To overcome this proble we have to create JSP page inside WEB-INF folder
* Only a servlet can run this file

**Header Menu**
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
</head>
<body>
	<a href="newRegistration">New Registration</a>
	<a href="readRegistration">View All Registrations</a>
	<form action="logout" method="post">
		<input type="submit" value="logout">
	</form>
</body>
</html>
```
### Registration ###
**View**
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ include file="Menu.jsp"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>New Registration</title>
</head>
<body>
<form action="newRegistration" method="post">
	Name: <input type="text" name="name"> <br>
	Course: <input type="text" name="course"> <br>
	Email: <input type="email" name="email"> <br>
	Mobile: <input size="10" type="number" name="mobile"> <br>
	<input type="submit" value="Save">
</form>
<%
	if(request.getAttribute("msg")!=null){
	out.print(request.getAttribute("msg"));
	}
%>
</body>
</html>
```

**Controller**
```java
package com.registration.controller;

import java.io.IOException;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import com.registration.module.DAOserviceIMPL;

@WebServlet("/newRegistration")
public class NewRegistrationController extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public NewRegistrationController() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/NewRegistration.jsp");
		rd.forward(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String name = request.getParameter("name");
		String course = request.getParameter("course");
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		HttpSession session = request.getSession(false);
		if (session.getAttribute("email") != null) {
			DAOserviceIMPL service = new DAOserviceIMPL();
			service.connectDB();
			service.createRegistration(name, course, email, mobile);
			request.setAttribute("msg", "Record Inserted Successfully");
			RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/NewRegistration.jsp");
			rd.forward(request, response);
		} else {
			request.setAttribute("msg", "Login to continue");
			RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
			rd.forward(request, response);
		}
	}

}

```
**Model**
```java
@Override
	public void createRegistration(String name, String course, String email, String mobile) {
		try {
			stmnt.executeUpdate("insert into registration values('"+name+"','"+course+"','"+email+"','"+mobile+"')");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
```
### Read Registration ###
**View**
```jsp
<%@page import="java.sql.ResultSet"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
    <%@ include file="Menu.jsp" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Read Registration</title>
</head>
<body>
	<table>
	<tr>
	<th>Name</th>
	<th>Course</th>
	<th>Email</th>
	<th>Mobile</th>
	<th>Update</th>
	<th>Delete</th>
	</tr>
	<% ResultSet result = (ResultSet)request.getAttribute("result");
	while(result.next()){
		%><tr>
		<td><%= result.getString(1) %> </td>
		<td><%= result.getString(2) %> </td>
		<td><%= result.getString(3) %> </td>
		<td><%= result.getString(4) %> </td>
		<td> <a href="updateRegistration?email=<%=result.getString(3)%>&mobile=<%=result.getString(4)%>">Update	</a> </td>
		<td> <a href="deleteRegistration?email=<%=result.getString(3)%>">Delete</a> </td>
		</tr>
	<%}
	%>
	</table>
</body>
</html>
```
**Controller**
```java
package com.registration.controller;

import java.io.IOException;
import java.sql.ResultSet;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import com.registration.module.DAOserviceIMPL;

@WebServlet("/readRegistration")
public class ReadRegistrationController extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public ReadRegistrationController() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		HttpSession session = request.getSession(false);
		if (session.getAttribute("email") != null) {
		DAOserviceIMPL service = new DAOserviceIMPL();
		service.connectDB();
		ResultSet result = service.retriveRegistration();
		request.setAttribute("result", result);
		RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/ReadRegistration.jsp");
		rd.forward(request, response);
		} else {
			request.setAttribute("msg", "Login to continue");
			RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
			rd.forward(request, response);
		}
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

	}

}

```
**Model**
```java
@Override
	public ResultSet retriveRegistration() {
		try {
			ResultSet result = stmnt.executeQuery("select * from registration");
			return result;
		} catch (Exception e) {
			e.printStackTrace();
		}
		return null;
	}
```

### Update Registration ###
**View**
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ include file="Menu.jsp"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>New Registration</title>
</head>
<body>
<form action="updateRegistration" method="post">
	Email: <input type="email" name="email" value="<%=request.getAttribute("email") %>" readonly="readonly"> <br>
	Mobile: <input type="number" name="mobile" value="<%=request.getAttribute("mobile") %>"> <br>
	<input type="submit" value="Update">
</form>

</body>
</html>
```
**Controller**
```java
package com.registration.controller;

import java.io.IOException;
import java.sql.ResultSet;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.registration.module.DAOserviceIMPL;


@WebServlet("/updateRegistration")
public class UpdateRegistrationController extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public UpdateRegistrationController() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		
		request.setAttribute("email", email);
		request.setAttribute("mobile", mobile);
		
		RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/UpdateRegistration.jsp");
		rd.forward(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		
		DAOserviceIMPL service = new DAOserviceIMPL();
		service.connectDB();
		service.updateRegistration(email, mobile);
		ResultSet result = service.retriveRegistration();
		request.setAttribute("result", result);
		RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/ReadRegistration.jsp");
		rd.forward(request, response);
	}

}

```

**Model**
```java
@Override
	public void updateRegistration(String email, String mobile) {
		try {
			int executeUpdate = stmnt.executeUpdate("update registration set mobile='"+mobile+"' where email='"+email+"'");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
```
### Delete Registration ##
**Controller**
```java
package com.registration.controller;

import java.io.IOException;
import java.sql.ResultSet;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.registration.module.DAOserviceIMPL;

@WebServlet("/deleteRegistration")
public class DeleteRegistrationController extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public DeleteRegistrationController() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String email = request.getParameter("email");
		DAOserviceIMPL service = new DAOserviceIMPL();
		service.connectDB();
		service.deleteRegistration(email);
		ResultSet result = service.retriveRegistration();
		request.setAttribute("result", result);
		RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/ReadRegistration.jsp");
		rd.forward(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		
		
	}

}

```
**Model**
```java
@Override
	public void deleteRegistration(String email) {
		try {
			stmnt.executeUpdate("delete from registration where email='"+email+"'");
		} catch (Exception e) {
			e.printStackTrace();
		}
		
	}
```
### LogOut ###
**Controller**
```java
package com.registration.controller;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;


@WebServlet("/logout")
public class LogoutController extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public LogoutController() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		HttpSession session = request.getSession(false);
		session.invalidate();
		request.setAttribute("msg", "Loged Out..!!");
		RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
		rd.forward(request, response);
	}

}

```