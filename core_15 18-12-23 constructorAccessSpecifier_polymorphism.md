####Default Constructor

* If you create default constructor in a class then its object can be created in same class & same package but not outside the package.

```java
package p1;
public class A {
	A(){
		
	}
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p1;
public class B {
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p2;
import p1.A;
public class C {
	A a1 = new A(); //Error
}
```

* If you create default constructor in a class then that class inheritance is allowed in same package but not in different package.

```java
package p1;
public class A {
	A(){
		
	}
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p2;
import p1.A;
public class C extends A{ //Error
	public static void main(String[] args) {
		
	}
}
```


####Protected Constructor
* If you create Protected constructor in a class then its object can be created in same and same package but not outside the package.

```java
package p1;
public class A {
	protected A(){
		
	}
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p1;
public class B {
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p2;
import p1.A;
public class C {
	public static void main(String[] args) {
		A a1 = new A(); //Error
	}
}
```

* if you created protected constructor in a class then that class inheritance is allowed in same package and in different package also.

```java
package p1;
public class A {
	protected A(){
		
	}
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		
	}
}
```

```java
package p2;
import p1.A;
public class C extends A {
	public static void main(String[] args) {
	}
}
```

####Public Constructor

* If you create d public constructor in a class then its object can be created in same class and same package

```java
package p1;
public class A {
	public A(){
		
	}
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p1;
public class B {
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p2;
import p1.A;
public class C{
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

* If you create public constructor in a class then that class in heritance is allowed in same package and ina different package also.
```java
package p1;
public class A {
	public A(){
		
	}
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		
	}
}
```

```java
package p2;
import p1.A;
public class C{
	public static void main(String[] args) {
	}
}
```

#Polymorphism
####Note

Polymorphism is applicable only on methods 
Here we develop features such that it can take more then one from depending on situation.

####Types of Polymorphism
1 : Compile-time Polymorphism (method overloading)
2 : Run-time Polymorphism (method overriding)

####Run-time Polymorphism (method overriding)
Here we inherit the method from parent class and then modify the logic on inherited method in the child class.

```java
package p1;
public class Dog {
	public void eat() {
		System.out.println("Eat");
	}
	public void Sleep() {
		System.out.println("Sleep");
	}
	public void noise() {
		System.out.println("Bow");
	}
}
```
```java
package p1;

public class Cat extends Dog{
	public void noise() {
		System.out.println("mow");
	}
	public static void main(String[] args) {
		Cat c =  new Cat();
		c.Sleep();
		c.eat();
		c.noise();
		
		Dog d =  new Dog();
		d.Sleep();
		d.eat();
		d.noise();
	}
}
```
