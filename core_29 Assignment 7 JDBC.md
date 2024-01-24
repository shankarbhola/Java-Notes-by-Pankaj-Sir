# JDBC # 
**Java Database Connectivity**

* MySQL Database
* MongoDB
* Apache Derby
* Oracle Database
* etc..

**MySQL Database Installation**
Go to https://dev.mysql.com/downloads/windows/installer/8.0.html
Download mysql-installer-community and install

* create new sql connection 
* login 

**Create new database**

```sql
create database db_1
```
**Use database**
```sql
use db_1
```
**Create a table**
```sql
create table student
(
    firstname varchar(20),
    lastname varchar(20),
    cource varchar(20),
    city varchar(20)
)
```
insert value in to table
```sql
insert into student values
(
	'bhola', 'shankar', 'fullstack', 'bangalore' 
)
```
**View Values**
```sql
select * from student
```

```mermaid
graph LR

A[Java Code <br>]
B[Database] 
C{{Connector J}}
A<--->C
C<--->B

```

Go to https://dev.mysql.com/downloads/connector/j/
Download connectoe J
* Extract the zip file 
* copy the mysql-connector-j jar file
* open eclips and create a java project
* create a folder named "lib" under the java project
* paste mysql-connector-j jar file inside lib folder

```java
import java.sql.*;

public class C {
	public static void main(String[] args) {
		Connection con;
		try {
			con = DriverManager.getConnection("jdbc:mysql://localhost:3306/db_1", "root", "system");
			System.out.println(con);
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
---
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
			stmnt.executeUpdate("insert into student values ('mike', 'chennai', 'mike@gmail.com', '123456789')");
			//close
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```