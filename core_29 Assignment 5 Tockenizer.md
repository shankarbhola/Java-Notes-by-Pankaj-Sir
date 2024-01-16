## a* ##

It gives zero occurances or group of occurances of a particular character
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("a*");
		Matcher m = p.matcher("aabaaababaaab");
		
		while (m.find()) {
			System.out.println(m.start()+"..."+m.group());
		}
	}
}
```
```java
OUTPUT
0...aa
2...
3...aaa
6...
7...a
8...
9...aaa
12...
13...
```
## a+ ##
It gives only group of occurances of a particular character
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("a+");
		Matcher m = p.matcher("aabaaababaaab");
		
		while (m.find()) {
			System.out.println(m.start()+"..."+m.group());
		}
	}
}
```

```java
OUTPUT
0...aa
3...aaa
7...a
9...aaa
```

## a+ ##

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("a?");
		Matcher m = p.matcher("aabaaababaaaab");
		
		while (m.find()) {
			System.out.println(m.start()+"..."+m.group());
		}
	}
}
```
```java
OUTPUT
0...a
1...a
2...
3...a
4...a
5...a
6...
7...a
8...
9...a
10...a
11...a
12...a
13...
14...

```

# Tokenizer #

```java
public class A {
	public static void main(String[] args) {
		StringTokenizer str = new StringTokenizer("Pankaj Sir Academy");
		while (str.hasMoreTokens()) {
			System.out.println(str.nextToken());
		}
	}
}
```
---
```java
import java.util.StringTokenizer;

public class A {
	public static void main(String[] args) {
		StringTokenizer str = new StringTokenizer("12-12-2020","-");
		int count = 0;
		while (str.hasMoreTokens()) {
			System.out.println(str.nextToken());
			count++;
		}
		System.out.println(count);
	}
}
```
### Cloning ###
The process of creating replica of a perticular object by copying the content of one object cmpletely into another object.
```java
public class A implements Cloneable {
	public static void main(String[] args) {
		A a1 = new A();

		try {
			A a2 = (A) a1.clone();
			System.out.println(a1);
			System.out.println(a2);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

**hashcode()**
hashcode() will return integer represent of memory address

```java
public class A {
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.hashCode());
	}
}

```