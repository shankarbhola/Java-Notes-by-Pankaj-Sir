**Servlet to database connection**
* copy the mysql connector jar and copy
* open the project then go to src > main > webapp > WEB-INF > lib then paste the jar file

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>New Registration</title>
</head>

<body>
    <h1>New Registration</h1>
    <form action="newReg" method="post">
        <table>
            <tr>
                <td>Name : </td>
                <td><input type="text" name="name"></td>
            </tr>
            <tr>
                <td>City : </td>
                <td><input type="text" name="city"></td>
            </tr>
            <tr>
                <td>email : </td>
                <td><input type="text" name="email"></td>
            </tr>
            <tr>
                <td>mobile</td>
                <td><input type="text" name="mobile"></td>
            </tr>
            <tr>
                <td>
                    <input type="submit" value="Save">
                </td>
            </tr>

        </table>
    </form>

</body>

</html>
```
```java
package p1;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/newReg")
public class newRegistration extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public newRegistration() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String name = request.getParameter("name");
		String city = request.getParameter("city");
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			Statement stmnt = con.createStatement();
			stmnt.executeUpdate("insert into registration values('"+name+"', '"+city+"', '"+email+"', '"+mobile+"')");
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

```
**Delete**
```html
<!DOCTYPE html>
<html>

<head>
	<meta charset="ISO-8859-1">
	<title>Delete registration</title>
</head>

<body>
	<form action="deleteReg" method="post">
		<table>
			<tr>
				<td>Email :</td>
				<td><input type="text" name="email"></td>
			</tr>
			<tr>
				<td>
					<input type="submit" value="Delete">
				</td>
			</tr>
		</table>
	</form>
</body>

</html>
```

```java
package p1;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/deleteReg")
public class deleteRegistration extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public deleteRegistration() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		String email = request.getParameter("email");

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db", "root", "system");
			Statement stmnt = con.createStatement();
			stmnt.executeUpdate("delete from registration where email='" + email + "'");
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}

	}

}

```

**UPDATE**
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="ISO-8859-1">
    <title>Insert title here</title>
</head>

<body>
    <form action="updateReg" method="post">
        <table>
            <tr>
                <td>Email :</td>
                <td><input type="text" name="email"></td>
            </tr>
            <tr>
                <td>Mobile</td>
                <td><input type="text" name="mobile"></td>
            </tr>
            <tr>
                <td><input type="submit" value="Update"></td>
            </tr>
        </table>
    </form>
</body>

</html>
```
```java
package p1;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.mysql.cj.jdbc.Driver;

@WebServlet("/updateReg")
public class updateRegistraion extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public updateRegistraion() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db", "root", "system");
			Statement stmnt = con.createStatement();
			stmnt.executeUpdate("update registration set mobile='" + mobile + "'where email='" + email + "'");
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

```