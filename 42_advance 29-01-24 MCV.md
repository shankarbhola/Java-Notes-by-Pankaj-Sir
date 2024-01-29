## Model Contriller View (MCV) Architecture ##
![picture](https://i.ibb.co/LvPNdMp/image.png)
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
	<form action="addController" method="post">
	<input type="text" name="num1"/>
	<input type="text" name="num2"/>
	<input type="submit" value="add"/>
	</form>
	<%
	if(request.getAttribute("res")!=null){
		
	out.println(request.getAttribute("res"));
	}
	
	%>
</body>
</html>
```

```java
package com.xyz.controller;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.xyz.model.AddNumber;

@WebServlet("/addController")
public class AddController extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public AddController() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		int num1 = Integer.parseInt(request.getParameter("num1"));
		int num2 = Integer.parseInt(request.getParameter("num2"));
		
		AddNumber add = new AddNumber();
		int result = add.addnum(num1, num2);
		
		request.setAttribute("res", result);
		RequestDispatcher rd = request.getRequestDispatcher("wlcm.jsp");
		rd.forward(request, response);
	}
}
```

```java
package com.xyz.model;

public class AddNumber {
	public int addnum(int x, int y) {
		return x+y;
	}
}

```