**Read data from Database**
```java
import java.sql.*;

public class C {
	public static void main(String[] args) {
		Connection con;
		try {
			con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db", "root", "system");
			System.out.println(con);

			Statement stmt = con.createStatement();
			ResultSet result = stmt.executeQuery("select * from registration");

			while (result.next()) {
				System.out.print(result.getString(1) + " ");
				System.out.print(result.getString(2) + " ");
				System.out.print(result.getString(3) + " ");
				System.out.print(result.getString(4) + " ");
				System.out.println(" ");
			}
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

## finally ##
* finally block is an extention of try catch
* any code that we write in finally block it will 100% run

```java
public class A {
	public static void main(String[] args) {
		try {
			int x = 10 / 0;
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			System.out.println("Will run");
		}
	}
}

```
**How to Stop finally block forcefully**
using System.exit(0);

```java
import java.sql.*;

public class B {
	public static void main(String[] args) {
		Connection con = null;;
		try {
			con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			System.out.println(con);
			
			Statement stmt = con.createStatement();
			stmt.executeUpdate("insert into registration values ('mark', 'delhi', 'mark@mail.com', '7854624225')");
			
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				con.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}
}
```