In the below program B.test2() during compilation is converted to A.test2() and B.x is converted to A.x
static members are not inherited.

```java
public class A {
	static int x =10;
	public static void test2() {
		System.out.println(30);
	}
}
```

```java
public class B extends A{
	public static void main(String[] args) {
		B.test2();
		System.out.println(B.x);
	}
}
```

* We cannot create static incomplete methods in interface
```java
public interface A{
	public static void test1();
}
```


* We can create complete methods & main method in an interface

```java
public interface A{
	final static int x =100;
	public static void test1() {
		System.out.println(100);
	}
	public static void main(String[] args) {
		A.test1();
		System.out.println(A.x);
	}
}
```

## Abstract Keyword in java ##

* Are used to define incomplete methods & classes
* In an interface it is optional to use abstract Keyword to delevop incomplete methods

```java
public interface A{
	public abstract void test1();
}
```

## Abstract class in java ##

* You can create both complete & incomplete methods in it.
* To create incomplete methods in an abstract class it is mandatory to use abstract Keyword

```java
abstract public class A{
	public abstract void test1();
	public void test2(); // Error because we have to use abstract keyword
}
```

----
```java
abstract public class A{
	public abstract void test1();
	public void test2(){
		System.out.println(2);
	}
}
```

```java
public class B extends A{
	@Override
	public void test1() {
		System.out.println(1);
	}
	public static void main(String[] args) {
		B b1 = new B();
		b1.test1();
		b1.test2();
	}
}
```

-----
```java
public interface A{
	public void test1();
}
```

```java
abstract public class B implements A {
	abstract public void test2();
}
```

```java
public class C extends B{
	@Override
	public void test1() {
		System.out.println(1);
	}
	@Override
	public void test2() {
		System.out.println(2);
	}
	public static void main(String[] args) {
		C c1 = new C();
		c1.test1();
		c1.test2();
	}
}
```

* Abstract class doesnot support multiple inheritance

```java
abstract public class A{

}
```

```java
abstract public class B {

}
```

```java
abstract public class C extends A,B{ //Error
	
} 
```


 We can create both static / non-static menbers in an abstract class 

### Note: ###
Ojbect of abstract class cannot be created, but reference variable of abstract class can be created 

```java
abstract public class A{
	int x = 10;
	static int y = 20;
}
```

```java
public class B extends A{
	public static void main(String[] args) {
		//A a1 = new A(); //Error
		B b1 = new B();
		System.out.println(b1.x);	
		System.out.println(A.y);
	}
}
```

-----

```java
abstract public class A{
	static int y = 20;
	public static void main(String[] args) {
		System.out.println(A.y);
		A.test();
	}
	
	public static void test() {
		System.out.println(200);
	}
}
```

### Difference between interface and abstract class ###

#### interface ####
* Supports multiple inheritance
* variables by default final and static 
* Interface can consist only incomplete method

#### abstract class ####

* doesnot support multiple inheritance
* variables can be static / non-static
* can consist incomplete method and complete method both


 Functional interface doesnot support multiple inheritance

```java
@FunctionalInterface
public interface A{
	public void test1();
}
```

```java
@FunctionalInterface
public interface B {
	public void test2();
}
```

```java
@FunctionalInterface
public interface C extends A,B{ //Error
	
}
```



