## throws ##
* It is applied on a method.
* In any Exception occurs in the methods then the exception will be passed on to the calling statement of the method.
  
```java
import java.io.FileWriter;

public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test(); //Unhandled Exception 
	}
	public void test() throws Exception {
		FileWriter fw = new FileWriter("E://reports.A.txt");
	}
}
```
```java
import java.io.FileWriter;

public class A {
	public static void main(String[] args) {
		A a1 = new A();
		try {
			a1.test();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
	public void test() throws Exception {
		FileWriter fw = new FileWriter("E://reports.A.txt");
	}
}
```
```java
import java.io.FileWriter;

public class A {
	public static void main(String[] args) throws Exception {
		A a1 = new A();
		a1.test();
	}
	public void test() throws Exception {
		FileWriter fw = new FileWriter("D://test//A.txt");
	}
}
```
## throw ##
* It helps us to create customized exception as per the requirement of the developer.

```java
import java.util.Scanner;

public class A {
	public static void main(String[] args) {
		int balance = 500;
		Scanner s = new Scanner(System.in);
		System.out.println("Enter the amount");
		int amount = s.nextInt();
		if (balance>amount) {
			System.out.println("Please collect your cash");
		} else {
			try {
				throw new InSufficientFunds();
			} catch (InSufficientFunds e) {
				System.out.println(e);
				System.out.println("Low balance !");
			}
		}
	}
}
```
---
```java
public class ApplicationCrashed extends Throwable {
	
}

```

```java
public class A {
	public static void main(String[] args) {
		try {
			throw new ApplicationCrashed();
		} catch (ApplicationCrashed e) {
			System.out.println(e);
			System.out.println("Application Restart");
		}
	}
}
```
---
```java
import java.io.FileWriter;
import java.io.IOException;
import java.sql.DriverManager;
import java.sql.SQLException;

public class A {
	public static void main(String[] args) throws SQLException, IOException {
		FileWriter fw = new FileWriter("D://test//A.txt");
		DriverManager.getConnection("", "", "");
	}
}
```