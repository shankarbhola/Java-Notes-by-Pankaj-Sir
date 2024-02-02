**MVC Mini Project**
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
	<form action="validateLogin" method="post">
		Email: <input type="text" name="email">
		<br>
		Password: <input type="password" name="pwd">
		<br>
		<input type="submit" value="login">
	</form>
</body>
</html>
```
**Controller**
```java
package com.registration.controller;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.registration.model.DAOserviceImpl;


@WebServlet("/validateLogin")
public class VerifyLogin extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public VerifyLogin() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String email = request.getParameter("email");
		String password = request.getParameter("pwd");
		
		DAOserviceImpl service = new DAOserviceImpl();
		service.connectDB();
		boolean verifyLogin = service.verifyLogin(email, password);
		boolean status = service.verifyLogin(email, password);
		
		if (status) {
			RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/view/newRegistration.jsp");
			rd.forward(request, response);
		} else {
			request.setAttribute("errmsg", "Invalid Username/Password");
			RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
			rd.forward(request, response);
		}
	}

}

```
**Model**
```java
package com.registration.model;

import java.sql.*;

public class DAOserviceImpl implements DAOservice {
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
			ResultSet result = stmnt.executeQuery("select * from login where email='"+email+"' and password = '"+password+"'");
			return result.next();
		} catch (Exception e) {
			e.printStackTrace();
		}
		return false;
	}

	@Override
	public void createRegistration(String name, String email, String cource, String mobile) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void deleteRegistration(String email) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void updateRegistration(String email, String mobile) {
		// TODO Auto-generated method stub
		
	}

}

```