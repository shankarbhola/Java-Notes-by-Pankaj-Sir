* Functional Interface
* Lambda Expression
* Default Keyword
* Optional class 
* Stream API

## Functional Interface ##
In an Functional Interface their should be exactly 1 incomplete method in it.

```java
@FunctionalInterface
public interface A { //Error
	
}
```
---
```java
@FunctionalInterface
public interface A { //Error
	public void test1();
	public void test2();
	
}
```
---
```java
@FunctionalInterface
public interface A { 
	public void test1();
	
}
```

```java
public class B implements A{

	@Override
	public void test1() {
		System.out.println("From Test1");
	}
	public static void main(String[] args) {
		B b1 = new B();
		b1.test1();
	}
}
```

### default Keyword ###
This was introduced in java versio 8. Using default keyword we can create complete methods in an interface.

```java
@FunctionalInterface
public interface A { 
	public void test1();
	default public void test2() {
		System.out.println("From Test2");
	}
}
```

```java
public class B implements A{

	@Override
	public void test1() {
		System.out.println("From Test1");
	}
	public static void main(String[] args) {
		B b1 = new B();
		b1.test1();
		b1.test2();
	}
}
```

---

```java
@FunctionalInterface
public interface A { 
	public void test1();
	default public void test2() {
		System.out.println("From Test2");
	}
	default public void test3() {
		System.out.println("From Test3");
	}
	default public void test4() {
		System.out.println("From Test4");
	}
}
```

```java
public class B implements A{

	@Override
	public void test1() {
		System.out.println("From Test1");
	}
	public static void main(String[] args) {
		B b1 = new B();
		b1.test1();
		b1.test2();
		b1.test3();
		b1.test4();
	}
}
```
----
```java
@FunctionalInterface
public interface A { 
	public void test1();
	default public int test2() {
		return 100;
	}
}
```

```java
public class B implements A{

	@Override
	public void test1() {
		System.out.println("From Test1");
	}
	public static void main(String[] args) {
		B b1 = new B();
		b1.test1();
		int val = b1.test2();
		System.out.println(val);
	}
}
```

## Lambda Expression ##

This was introduced in java version 8. It helps to reduce the number pof lines of code in program.

```java
@FunctionalInterface
public interface A { 
	public void test1();
	
}
```

```java
public class B{

	public static void main(String[] args) {
		A a1=()->{
			System.out.println(100);
		};
		a1.test1();
	}
}
```

-----
```java
@FunctionalInterface
public interface A { 
	public void test1(int x);
	
}
```

```java
public class B{

	public static void main(String[] args) {
		A a1=(int x)->{
			System.out.println(x);
		};
		a1.test1(100);
	}
}
```
-----
```java
@FunctionalInterface
public interface A { 
	public void test1(int x, int y);
	
}
```

```java
public class B{

	public static void main(String[] args) {
		A a1=(int a, int b)->{
			System.out.println(a);
			System.out.println(b);
		};
		a1.test1(100,200);
	}
}
```
-----
```java
@FunctionalInterface
public interface A { 
	public void test1(int x, int y);
	default public void test2() {
		System.out.println(30);
	}
}
```

```java
public class B{

	public static void main(String[] args) {
		A a1=(int a, int b)->{
			System.out.println(a);
			System.out.println(b);
		};
		a1.test1(10,20);
		a1.test2();
	}
}
```
