```html
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Login</title>
</head>
<body>
	<form action="validatelogin" method="post">
        Email : <br> <input type="email" name="email"><br>
        Password : <br> <input type="password" name="password"><br>
        <br><input type="submit" value="Login">
    </form>
</body>
</html>
```
```java
package p1;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/validatelogin")
public class Loginvalidate extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public Loginvalidate() {
        super();
    }
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String email = request.getParameter("email");
		String password = request.getParameter("password");
		
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			
			Statement stmnt = con.createStatement();
			ResultSet result = stmnt.executeQuery("select * from login where email='"+email+"' and password = '"+password+"'");
			
			if (result.next()) {
				System.out.println("Welcome");
			}
			else {
				System.out.println("Wrong id / password");
			}
			
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
		
	}

}

```