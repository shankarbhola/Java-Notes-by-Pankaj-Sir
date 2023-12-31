```java
package p1;
public class GoldAccount {
	public void onlineBanking() {
		System.out.println("Yes");
	}
	public void rateOfInterest() {
		System.out.println("Nil");
	}
}
```

```java
package p1;
public class PlatinumAccount extends GoldAccount{
	public void rateOfInterest() {
		System.out.println("5% PA");
	}
	public static void main(String[] args) {
		PlatinumAccount p = new PlatinumAccount();
		p.onlineBanking();
		p.rateOfInterest();
		System.out.println("_______________");
		GoldAccount g = new GoldAccount();
		g.onlineBanking();
		g.rateOfInterest();
	}
}
```

####Note

@Override annotation will intruct compiler to check whether Override is happening or not.

```java
package p1;
public class A {
	public void test1() {
		
	}
}
```

```java
package p1;
public class B extends A{
	@Override
	public void test() { //Error
		
	}
}
```

* Scope of access specifier in child class can be incresed but shoud not be decresed during Overridinh.

```java
package p1;
public class A {
	public void test1() {
		
	}
}
```

```java
package p1;
public class B extends A{
	@Override
	 void test1() { //Error
		
	}
}
```
-----
```java
package p1;
public class A {
	void test1() {
		
	}
}
```

```java
package p1;
public class B extends A{
	@Override
	public void test1() { 
		
	}
}
```
-----
```java
package p1;
public class A {
	public int test1() {
		return 100;
	}
}
```

```java
package p1;
public class B extends A{
	@Override
	public void test1() { //Error
		
	}
}
```
-----
```java
package p1;
public class A {
	public int test1() {
		return 100;
	}
}
```

```java
package p1;
public class B extends A{
	@Override
	public int test1() { 
		return 200;
	}
}
```

####Compile-time Polymorphism (method overloading)

Here we create more then one method with same name in same class provided they have different number of arguments or different types of arguments

```java
package p1;
public class A {
	public void test() {// args = 0
		System.out.println(1);
	}
	public void test(int x) {// args = 1
		System.out.println(x);
	}
	public static void main(String[] args) {
		A a1 = new A();
		a1.test();
		a1.test(2);
	}
}
```

```java
package p1;
public class A {
	public void sendEmail() {
		System.out.println("Without attachment");
	}
	public void sendEmail(String path) {
		System.out.println("With attachment");
	}
	public static void main(String[] args) {
		A a1 = new A();
		a1.sendEmail();
		a1.sendEmail("G:/test.txt");
	}
}
```
