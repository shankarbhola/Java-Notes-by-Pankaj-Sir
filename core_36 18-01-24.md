Create a Dynamic web project
go to project > src > main > webapp then create a html file

```html
<!DOCTYPE html>
<html>

<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>

<body>
	<form action="newReg" method="post">
		<table>
			<tr>
				<td>Name:</td>
				<td><input type="text" name="name"></td>
			</tr>
			<tr>
				<td>city:</td>
				<td><input type="text" name="city"></td>
			</tr>
			<tr>
				<td>email:</td>
				<td><input type="text" name="email"></td>
			</tr>
			<tr>
				<td>Mobile:</td>
				<td><input type="text" name="mobile"></td>
			</tr>
			<tr>
				<td><input type="submit" value="save"></td>
			</tr>

		</table>
	</form>
</body>

</html>
```

* Go to project > Java Resources > src > main > java > package create a java servlet.

```java
package p1;

import java.io.IOException;
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
    
    @Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("Get");
	}
    @Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String name = request.getParameter("name");
		String city = request.getParameter("city");
		String email = request.getParameter("email");
		String mobile = request.getParameter("mobile");
		System.out.println(name);
		System.out.println(city);
		System.out.println(email);
		System.out.println(mobile);
		
	}

}

```