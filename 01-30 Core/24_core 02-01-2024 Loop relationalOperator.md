### Relational Operator ###

```java
public class A {
	public static void main(String[] args) {
		System.out.println(2==2);
		System.out.println(3>2);
		System.out.println(3<2);
		System.out.println(3>=3);
		System.out.println(3<=2);
		System.out.println(3!=2);
	}
}
```

### LOOP ###
**For Loop**
```java
import java.util.Scanner;

public class A {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);

		for (int i = 0; i < 3; i++) {
			System.out.println("Enter Pin Number");
			int pinNumber = scan.nextInt();
			if (pinNumber == 1234) {
				System.out.println("Welcome");
				break;
			} else {
				System.out.println("Invalid Pin Number");
				if (i == 2) {
					System.out.println("Card is Blocked");
				}
			}
		}
	}
}
```
**While Loop**

```java
public class B {
	public static void main(String[] args) {
		int x = 0;
		while (x<3) {
			System.out.println(x);
			x++;
		}
	}
}
```
---
```java
import java.util.Scanner;

public class A {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		String cdn = "yes";
		while (cdn.equals("yes")) {
			System.out.println("Enter the Amount");
			int amount = scan.nextInt();
			System.out.println("Please collect cash Rs "+amount);
			System.out.println("Do you want to continue (yes/no) ?");
			cdn = scan.next();
		}
	}
}

```
**do while**
```java
public class A {
	public static void main(String[] args) {
		int x = 0;
		do {
			System.out.println(x);
			x++;
		} while (x<3);
	}
}
```
**else if**
```java
public class A {
	public static void main(String[] args) {
		int x = 300;
		if (x == 10) {
			System.out.println(1);
		}
		else if (x == 20) {
			System.out.println(2);
		}
		else if (x == 30) {
			System.out.println(3);
		}
		else {
			System.out.println("No records found");
		}
	}
}```
