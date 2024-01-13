**Find white space in given string**

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		//lower case s
		Pattern p = Pattern.compile("\\s");
		Matcher m = p.matcher("a6b@# 9 D E !");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}

```
**Except white space**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		//upper case S
		Pattern p = Pattern.compile("\\S");
		Matcher m = p.matcher("a6b@# 9 D E !");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}
```
**Find digits**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("\\d");
		Matcher m = p.matcher("a6b@# 9 D E !");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}

```
**Except digit**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("\\D");
		Matcher m = p.matcher("a6b@# 9 D E !");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}

```
**find only lower case, uppercase and digits**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
        //lower case w
		Pattern p = Pattern.compile("\\w");
		Matcher m = p.matcher("a6b@# 9 D E !");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}

```
**find except lower case, uppercase and digits**
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Pattern p = Pattern.compile("\\W");
		Matcher m = p.matcher("a6b@# 9 D E !");
		while (m.find()) {
			System.out.println(m.start()+"...."+m.group());
		}
	}
}

```

**Checking Name**
```java
import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class A {
	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		System.out.println("Enter your Name :");
		String str = s.next();
		Pattern p = Pattern.compile("[^a-zA-z]");
		Matcher m = p.matcher(str);
		int count = 0;
		while (m.find()) {
			count ++;
		}
		
		if (count!=0 || str.length()<3) {
			System.out.println("Error");
		} else {
			System.out.println("Input Accepted");
		}
	}
}
```
**mobile number validation**
```java
import java.util.Scanner;

public class A {
	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		System.out.println("Enter Mobile Number :");
		String str = s.next();
		
		String regex = "[6-9][0-9]{9}";
		
		if (str.matches(regex)) {
			System.out.println("Valid");
		} else {
			System.out.println("invalid");
		}
	}
}

```