**Linking jar file to java project**
* Right click on project
* Go to properties
* Go to Java Build Path
* click on Libraries
* Select Jre system library 
* Select module path
* on the right side click add jars..
* select the mysql-connetor-j jar file 
* apply and close

```java
import java.sql.*;

public class A {
	public static void main(String[] args) {
		
		try {
			//connect to database
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			System.out.println(con);
			
			//execute 
			Statement stmnt = con.createStatement();
			stmnt.executeUpdate("insert into registration values ('mike', 'chennai', 'mike@gmail.com', '123456789')");
			//close
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```
**Delete record**
```java
import java.sql.*;

public class A {
	public static void main(String[] args) {
		
		try {
			//connect to database
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			System.out.println(con);
			
			//execute 
			Statement stmnt = con.createStatement();
			stmnt.executeUpdate("delete from registration where email='mike@gmail.com' " );
			//close
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

```java
import java.sql.*;

public class A {
	public static void main(String[] args) {
		
		try {
			//connect to database
			Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/nov_db","root","system");
			System.out.println(con);
			
			//execute 
			Statement stmnt = con.createStatement();
			stmnt.executeUpdate("update registration set mobile='9632629455' where email='adam@gmail.com' " );
			//close
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```