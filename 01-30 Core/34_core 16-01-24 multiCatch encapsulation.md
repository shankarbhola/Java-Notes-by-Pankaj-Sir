### Multi catch Block ###

```java
public class A{
	int y = 100;
	public static void main(String[] args) {
		try {
			A a1 = null;
			System.out.println(a1.y);
			int x = 10/0;
			Integer.parseInt("knuybrjyt7657");
		} catch (NumberFormatException e) {
			System.out.println(1);
		}
		catch (ArithmeticException e) {
			System.out.println(2);
		}
		catch (Exception e) {
			System.out.println(3);
		}
	}
}
```
# Encapsulation #
* Wrapping of data with methods such that the methods operate on that data is called Encapsulation
* Here we create private variables(data hiding) so that direct access to that is avoided.
* To operate on those variables publicly defined getters and settors.

```java
public class A {
	private String password;

	public String getPassword() {
		return password;
	}

	public void setPassword(String password) {
		this.password = password;
	}

}
```
```java
import java.io.BufferedReader;
import java.io.FileReader;

public class B {
	public static void main(String[] args) {
		try {
			FileReader fr = new FileReader("D://test//A.txt");
			BufferedReader br = new BufferedReader(fr);
			A a1 = new A();
			a1.setPassword(br.readLine());
			System.out.println(a1.getPassword());
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
---
```java
public class A {
	private int id;
	private String username;
	private String password;
	private boolean active;
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getUsername() {
		return username;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
	public boolean isActive() {
		return active;
	}
	public void setActive(boolean active) {
		this.active = active;
	}

}
```
```java
public class B {
	public static void main(String[] args) {
		A a1 = new A();
		a1.setId(10);
		a1.setUsername("jhon");
		a1.setPassword("jhon@123");
		a1.setActive(true);
		
		System.out.println(a1.getId());
		System.out.println(a1.getUsername());
		System.out.println(a1.getPassword());
		System.out.println(a1.isActive());
	}
}

```