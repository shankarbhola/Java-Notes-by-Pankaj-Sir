# JSP #

![picture](https://i.ibb.co/t2dKGkV/Untitled.png)

**1. Scriptlet Tag**
```jsp
<% 


%>
```
* cannot create html insite Scriptlet tag
* cannot use access specifier inside Scriptlet tag
* cannot create static/ non-static variables
* cannot create static/ non-static methods
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
<% 
System.out.println("Hello");
%>
</body>
</html>
```
![picture](https://i.ibb.co/N2m5pcC/Untitled.png)
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
<% 
	out.println("Hello");
request.setAttribute("msg", 100);
out.println(request.getAttribute("msg"));

session.setAttribute("sessonval", 200);
out.println(session.getAttribute("sessonval"));
%>
</body>
</html>
```
**2. Declaration Tag**
```jsp
<%!


%>
```
![picture](https://i.ibb.co/SwsS5mf/1.png)
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
	<%!
	public int x = 10;

	public int test() {
		return 100;
	}
	static int y = 20;
	%>
	
	<%
	out.println(x);
	out.println(test());
	out.println(y);
	%>
</body>
</html>
```

**3. Expression Tag**
```jsp
<%=      %> --> out.println();
```

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
	<%!
	public int x = 10;

	public int test() {
		return 100;
	}
	static int y = 20;
	%>
	
	<%= x %>
	<%= y %>
	<%= test() %>
</body>
</html>
```
**4. Directive Tag**
1. Page Directive tag - Used to perform imports

```jsp
<%@page import="web_app_3.A"%>
```
```jsp
<%@page import="web_app_3.A"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	
	<% 
		A a1 = new A();
	%>
</body>
</html>
```

2. Include Directive tag - Used to perform imports
```jsp
<%@include file="Test.txt" %>
```
```jsp
<%@page import="web_app_3.A"%>
<%@include file="Test.txt" %>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	
</body>
</html>

```