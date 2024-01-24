**InterServlet communication**
![picture](https://i.ibb.co/LdskZbN/1.png)


```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form action="first" method="post">
	name : <br>
	<input type="text" name="name"/> <br>
	<input type="submit" value="click" />
	</form>
</body>
</html>
```
First Servlet
```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/first")
public class firstServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public firstServlet() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		RequestDispatcher rd = request.getRequestDispatcher("second");
		rd.forward(request, response);
		
	}

}

```
Second Servlet
```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/second")
public class secondServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public secondServlet() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("Second Servlet");
	}
}

```
---
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form action="first" method="get">
	name : <br>
	<input type="text" name="name"/> <br>
	<input type="submit" value="click" />
	</form>
</body>
</html>
```

```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/first")
public class firstServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public firstServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		RequestDispatcher rd = request.getRequestDispatcher("second");
		rd.forward(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
				//inter servlet communication
		RequestDispatcher rd = request.getRequestDispatcher("second");
		rd.forward(request, response);

	}

}

```
```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/second")
public class secondServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public secondServlet() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("Second Servlet Get");
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("Second Servlet Post");
	}
}

```
---
Send Data from first servlet to second servlet
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form action="first" method="post">
	name : <br>
	<input type="text" name="name"/> <br>
	city : <br>
	<input type="text" name="city"/> <br>
	<input type="submit" value="click" />
	</form>
</body>
</html>
```

```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/first")
public class firstServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public firstServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String name = request.getParameter("name");
		String city = request.getParameter("city");
		request.setAttribute("x", name);
		request.setAttribute("y", city);

		RequestDispatcher rd = request.getRequestDispatcher("second");
		rd.forward(request, response);

	}

}

```
```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/second")
public class secondServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public secondServlet() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("Second Servlet Get");
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String name = request.getAttribute("x").toString();
		String city = (String)request.getAttribute("y");
		System.out.println(name);
		System.out.println(city);
	}
}

```
**Session Variables**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form action="first" method="post">
	name : <br>
	<input type="text" name="name"/> <br>
	city : <br>
	<input type="text" name="city"/> <br>
	<input type="submit" value="click" />
	</form>
</body>
</html>
```

```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/first")
public class firstServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public firstServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		RequestDispatcher rd = request.getRequestDispatcher("welcome.html");
		rd.forward(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String name = request.getParameter("name");
		String city = request.getParameter("city");
		request.setAttribute("x", name);
		request.setAttribute("y", city);
		
		HttpSession session = request.getSession();
		session.setAttribute("XSession", name);
		session.setAttribute("YSession", city);
		
		RequestDispatcher rd = request.getRequestDispatcher("second");
		rd.forward(request, response);

	}

}

```

```java
package p1;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/second")
public class secondServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public secondServlet() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String name = (String)request.getAttribute("x");
		String city = (String)request.getAttribute("y");
		
		HttpSession session = request.getSession();
		String XSession = (String)session.getAttribute("XSession");
		String YSession = (String)session.getAttribute("YSession");
		
		System.out.println(XSession);
		System.out.println(YSession);
		
		System.out.println(name);
		System.out.println(city);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String name = (String)request.getAttribute("x");
		String city = (String)request.getAttribute("y");
		
		HttpSession session = request.getSession();
		String XSession = (String)session.getAttribute("XSession");
		String YSession = (String)session.getAttribute("YSession");
		
		System.out.println(XSession);
		System.out.println(YSession);
		
		System.out.println(name);
		System.out.println(city);
	}
}

```