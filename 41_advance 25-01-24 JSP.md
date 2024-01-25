# JSP #

![picture](https://i.ibb.co/t2dKGkV/Untitled.png)

1. Scriptlet Tag
```java
<% 


%>
```
* cannot create html insite Scriptlet tag
* cannot use access specifier inside Scriptlet tag
* cannot create static/ non-static variables
* cannot create static/ non-static methods
```js
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
```js
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