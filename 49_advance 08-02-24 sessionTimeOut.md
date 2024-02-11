**session.setMaxInactiveInterval(10)**
after 10 second the session variable will be null
set this everywhere

**LoginController**
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
			HttpSession session = request.getSession(true);
			session.setAttribute("email", email);
			session.setMaxInactiveInterval(10);
			
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
**New Registration**
It will throw null pointer exception
so surround all the code inside try catch block
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
		try {
			String name = request.getParameter("name");
			String course = request.getParameter("course");
			String email = request.getParameter("email");
			String mobile = request.getParameter("mobile");
			HttpSession session = request.getSession(false);
			session.setMaxInactiveInterval(10);
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
		} catch (Exception e) {
			request.setAttribute("msg", "Session time out...!!");
			RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
			rd.forward(request, response);
		}
	}

}
```
**Read Registration**
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
		try {
			HttpSession session = request.getSession(false);
			session.setMaxInactiveInterval(10);
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
		} catch (Exception e) {
			e.printStackTrace();
			request.setAttribute("msg", "Session time out...!!");
			RequestDispatcher rd = request.getRequestDispatcher("login.jsp");
			rd.forward(request, response);
		}
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

	}

}
```

**Difference between doGet and doPost**
![picture](https://i.ibb.co/M9qd3GC/image.png)


**Difference between Application Sever and Web Server**
![picture](https://i.ibb.co/P1MpZMF/image.png)