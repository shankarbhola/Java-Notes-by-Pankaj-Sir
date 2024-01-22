**Print data on html husing servlet**
```java
package p1;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/outReg")
public class outRegistration extends HttpServlet {
	private static final long serialVersionUID = 1L;


    public outRegistration() {
        super();
    }

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		PrintWriter out = response.getWriter();
		out.print("<table>");
		out.print("<tr>");
		out.print("<th>");
		out.print("Name");
		out.print("</th>");
		out.print("<th>");
		out.print("City");
		out.print("</th>");
		out.print("<th>");
		out.print("Email");
		out.print("</th>");
		out.print("<th>");
		out.print("Mobile");
		out.print("</th>");
		out.print("<tr>");
		
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			Statement stmnt = con.createStatement();
			ResultSet Result = stmnt.executeQuery("select * from registration");
			while (Result.next()) {
				out.print("<tr>");
				out.print("<td>");
				out.print(Result.getString(1));
				out.print("</td>");
				out.print("<td>");
				out.print(Result.getString(2));
				out.print("</td>");
				out.print("<td>");
				out.print(Result.getString(3));
				out.print("</td>");
				out.print("<td>");
				out.print(Result.getString(4));
				out.print("</td>");
				out.print("<tr>");
			}
			
		} catch (Exception e) {
			e.printStackTrace();
		}
		out.print("</table>");
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

	}

}

```