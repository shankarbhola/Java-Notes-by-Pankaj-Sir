#### Reverse a given String ####

```java
public class A {
    public static void main(String[] args) {
    	String str = "pankaj sir academy";
    	for (int i = str.length()-1; i >= 0 ; i--) {
    		System.out.print(str.charAt(i));
		}
    }
}
```

#### count the number of words in the given string ####

```java
public class A {
    public static void main(String[] args) {
    	String str = "pankaj sir academy";
    	String[] s = str.trim().split(" ");
    	System.out.println(s.length);
    	for (String x : s) {
    		System.out.println(x);
		}
    }
}
```

---
#### write a program to check the opening bracket( and the closing bracket ) are same or not ####


```java
import java.util.Scanner;
public class A {
    public static void main(String[] args) {
    	Scanner scan = new Scanner(System.in);
    	System.out.println("Enter opening and closing paranthesis - ( )");
    	String str = scan.next();
    	int count1 = 0;
    	int count2 = 0;
    	for (int i = 0; i < str.length(); i++) {
			if (str.charAt(i)== '(') {
				count1++;
			} else if(str.charAt(i)== ')'){
				count2++;
			}
		}
    	
    	if (count1 == count2) {
			System.out.println("No Error");
		} else {
			System.out.println("Error");
		}
    }
}
```

## Star pattern ##
#### Square box ####

```java
public class A {
	public static void main(String[] args) {
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < 5; j++) {
				System.out.print("*");
			}
			System.out.print("\n");
		}
	}
}
```

----
```java
public class A {
	public static void main(String[] args) {
		for (int i = 0; i < 5; i++) {
			for (int j = 0; j < 5; j++) {
				if (i==0 && j==1 
					|| i==0 && j==2
					|| i==0 && j==3
					|| i==0 && j==4
					|| i==1 && j==2
					|| i==1 && j==3
					|| i==1 && j==4) {
					System.out.print(" ");
				} else {
					System.out.print("*");
				}
			}
			System.out.print("\n");
		}
	}
}