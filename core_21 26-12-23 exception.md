# Exception #

* When a bad user input is given program execution will stop abruptly

```java
public class A{
	public static void main(String[] args) {
		int x = 10;
		int y = 0;
		int z = x/y; //stops here
		System.out.println("Welcome");
	}
}
```

## Exception handling
* we handle exception in java using try{ }catch{} block
* If any exception occurs in try block then try vlock will create exception object & it will give that object's address to catch block. Catch block will supress that exception and further program will continue to run.

```java
public class A{
	public static void main(String[] args) {
		try {
			int x = 10;
			int y = 0;
			int z = x/y; //stops here
			System.out.println(100);
		} catch (Exception e) {
			System.out.println(e);
		}
		System.out.println("Welcome");
	}
}
```
---
```java
public class A{
	public static void main(String[] args) {
		try {
			int x = 10;
			int y = 0;
			int z = x/y; //stops here
			System.out.println(100);
		} catch (Exception e) {
			e.printStackTrace();
		}
		System.out.println("Welcome");
	}
}
```

### Types of exception ###

(1) Checked Exception / Compile-time Exception
(2) Unchecked Exception / RUn-time Exception

### (1) Checked Exception / Compile-time Exception ###

-> Checked or Compile-time exception will occur when .java file is converted to .class file or in otherways these exceptions occur during compilation of the program.
-> These exceptions are also called as checked exception.

### (2) Unchecked Exception / RUn-time Exception ###

It will occur when we run .class file or in other words this exception occur duting runtime of the program. These exceptions are alsocalled as unchecked exceptions.