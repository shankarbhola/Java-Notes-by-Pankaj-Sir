## Regular Expression in Java ##

![picture](https://i.ibb.co/QmmJ63v/Untitled.png)

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("[abcd]");
		Matcher m = p.matcher("a6b#@z9Dcd");
		while (m.find()) {
			System.out.println(m.group()+"...."+m.start());
		}
	}
}

```
---
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("[a-z]");
		Matcher m = p.matcher("a6b#@z9Dcd7efX");
		while (m.find()) {
			System.out.println(m.group()+"...."+m.start());
		}
	}
}
```
---
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("[0-9]");
		Matcher m = p.matcher("a6b#@z9Dcd7efX");
		while (m.find()) {
			System.out.println(m.group()+"...."+m.start());
		}
	}
}
```
---
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("[a-zA-Z0-9]");
		Matcher m = p.matcher("a6b#@z9Dcd7efX");
		while (m.find()) {
			System.out.println(m.group()+"...."+m.start());
		}
	}
}
```
---
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("[^a-z]");
		Matcher m = p.matcher("a6b#@z9Dcd7efX");
		while (m.find()) {
			System.out.println(m.group()+"...."+m.start());
		}
	}
}
```
---
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("[0-9]{10}");
		Matcher m = p.matcher("9632882052");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}
```
