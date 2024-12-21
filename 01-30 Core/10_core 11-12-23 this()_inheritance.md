## this() ##
* Is used to call a constructor from another constructor

```java
package p1;
public class A { 
	  A(){
		  System.out.println("A");
	  }
	  A(int x){
		  this();
	  }
	  public static void main(String[] args) {
		A a1 = new A(100);
	}
}
```
---
```java
package p1;
public class A { 
	  A(){
		  this(100);
	  }
	  A(int x){
		  System.out.println("A");
	  }
	  public static void main(String[] args) {
		A a1 = new A();
		
	}
}
```
```java
package p1;
public class A { 
	  A(){
		  this(100);
	  }
	  A(int x){
		  this(1000,2000);
	  }
	  A(int x, int y){
		  System.out.println(x);
		  System.out.println(y);
	  }
	  public static void main(String[] args) {
		A a1 = new A();
	}
}
```
## Constructor Chaining ##

When you call one constructor from another constructor 

```java
package p1;
public class A { 
	  A(){
		  System.out.println(100);
	  }
	  A(int x){
		  A a2 = new A();
	  }
	  public static void main(String[] args) {
		A a1 = new A(100);
	}
}
```

* While calling a constructor this() keyword should always be first statement inside another constructor.
```java
package p1;
public class A { 
	  A(){
		  System.out.println(100);
	  }
	  A(int x){
		  System.out.println(200);
		  this(); //Error
	  }
	  public static void main(String[] args) {
		A a1 = new A(100);
	}
}
```

# OOPS #
## Inheritance ##
Here we inherit the members of parent class to child class so that we can reuse these members.

```java
package p1;
public class Animal {
	public void eat() {
		System.out.println("Eating");
	}
	public void sleep() {
		System.out.println("Sleeping");
	}
	public void walk() {
		System.out.println("Walking");
	}
}
```
---
```java
package p1;
public class Cat extends Animal{
	public void noise() {
		System.out.println("Mew");
	}
	public static void main(String[] args) {
		Cat cat = new Cat();
		cat.eat();
		cat.sleep();
		cat.walk();
		cat.noise();
	}
}
```
