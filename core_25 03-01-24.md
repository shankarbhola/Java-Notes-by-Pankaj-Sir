```java
public class A {
	public static void main(String[] args) {
	for (int i = 0; i < 5; i++) {
		if(i==2) {
			break;
		}
		System.out.println(i);
	}
	}
}
```
---
```java
public class A {
	public static void main(String[] args) {
	for (int i = 0; i < 5; i++) {
		if(i==2) {
			continue;
		}
		System.out.println(i);
	}
	}
}
```
* When continue run it go back to for loop
* break will exit the for loop continue put you back to the for loop

```java
public class A {
	public static void main(String[] args) {
		int x = -1;
		while (x < 3) {
			x++;
			if (x == 1) {
				continue;
			}
			System.out.println(x);
		}
	}
}
```
---
```java
public class A {
	public static void main(String[] args) {
		for (int i = 0; i < 5; i++) {
			out: if (i == 2) {
				break out;
			}
			System.out.println(i);
		}
	}
}
```
