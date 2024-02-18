### Lower case and Upper case ####

```java
final public class A {
	public static void main(String[] args) {
		String str = "Pankaj Sir AcAadeMy";
		System.out.println(str.toLowerCase());
		System.out.println(str.toUpperCase());
	}
}
```

### remove white space ###

```java
final public class A {
	public static void main(String[] args) {
		String str = "        Pankaj Sir AcAadeMy       ";
		System.out.println(str);
		System.out.println(str.trim());
	}
}
```

### check string start and ends with ###
```java
final public class A {
	public static void main(String[] args) {
		String str = "aabbababaabbaz";
		System.out.println(str.startsWith("a"));
		System.out.println(str.endsWith("z"));
		System.out.println(str.startsWith("x"));
		System.out.println(str.endsWith("x"));
	}
}
```

### check string length ###

```java
final public class A {
	public static void main(String[] args) {
		String str = "aabbababaabbaz";
		System.out.println(str.length());
	}
}
```

### ValueOf() ###

ValueOf  method converts given type such as int, long, float, double, boolean, and char array to string  

```java
final public class A {
	public static void main(String[] args) {
		int  i = 10;
		String str = String.valueOf(i);
		System.out.println(str);
	}
}
```

---
```java
final public class A {
	public static void main(String[] args) {
		char[]  i = {'a', 'b', 'c'};
		String str = String.valueOf(i);
		System.out.println(str);
	}
}
```

#### Wap to find how may letter 'a' and 'b' in the given string aabaaaababa ####
```java
public class A {

	public static void main(String[] args) {
		String str = "aabaaaababa";
		int a = 0;
		int b = 0;
		for (int i = 0; i < str.length(); i++) {
			if (str.charAt(i) == 'a') {
				a++;
			} else if (str.charAt(i) == 'b') {
				b++;
			}
		}
		System.out.println("Number of a : " + a);
		System.out.println("Number of b : " + b);
	}
}
```

### find duplicate elements in the given array ###
```java
public class A {

	public static void main(String[] args) {
		char[] x = { 'a', 'c', 'b', 'a', 'c' };
		System.out.println("repeated elements are");
		for (int i = 0; i < x.length; i++) {
			for (int j = 0; j < i; j++) {
				if (x[i] == x[j]) {
					System.out.println(x[i]);
					break;
				}
			}
		}
	}
}

```
