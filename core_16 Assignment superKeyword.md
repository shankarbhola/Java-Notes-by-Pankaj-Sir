Super keyword
-------------
* In java parent class also we call it as super class
* using super keyword you will be able to access members of parent class
* super keyword can be used only when inheritance is happening

* Using super keyword we can access the members of parent class
```java
package p1;
public class A {
	int i = 10;
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		B b1 = new B();
		b1.test();
	}
	public void test() {
		System.out.println(super.i);
	}
}
```
------
```java
package p1;
public class A {
	public void xyz() {
		System.out.println("xyz");
	}
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		B b1 = new B();
		b1.test();
		
	}
	public void test() {
		super.xyz();
	}
}
```


####Note

* Using super keyword we can access static and non static members also.
```java
package p1;
public class A {
	static int j = 10;
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		B b1 = new B();
		b1.test();
		
	}
	public void test() {
		System.out.println(super.j);
	}
}
```
* super keyword cannot be used inside static context
```java
package p1;
public class A {
	static int j = 10;
}
```

```java
package p1;
public class B extends A{
	public static void main(String[] args) {
		B b1 = new B();
		b1.test();
		
	}
	public static void test() {
		System.out.println(super.j); //Error
	}
}
```


* Using super keyword we can call constructor of parent class but then we should use super keyword in child class constructor and it should be the very fast statement

```java
package p1;
public class A {
	A(){
		System.out.println("A");
	}
}
```

```java
package p1;
public class B extends A {
	B() {
		super();
	}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```
-----
```java
package p1;
public class A {
	A(){
		System.out.println("A");
	}
}
```

```java
package p1;
public class B extends A {
	B() {
        System.out.println("B");
		super(); //Error
	}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```

* If we dont keep super keyword inside child class constructor then compiler will automatically place the super keyword such that it can call only no args constructor of parent class.

```java
package p1;
public class A {
	A(){
		System.out.println("A");
	}
}
```

```java
package p1;
public class B extends A {
	B() {
        
	}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```

* If you dont create child class constructor without argument then compiler will automatically placed no args constructor along with super keyword

```java
package p1;
public class A {
	A(){
		System.out.println("A");
	}
}
```

```java
package p1;
public class B extends A {
    //B{placed by constructor
		//super(); placed by constructor
	//}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```
-----
```java
public class A {
	A(){
		System.out.println("A");
	}
}
```

```java
package p1;
public class B extends A {
	B() {
        //super(); placed by constructor
        System.out.println("B");
	}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```
-----
```java
public class A {
	A(){
		System.out.println("A");
	}
}
```

```java
package p1;
public class B extends A {
	B(int i) {
        //super(); placed by constructor
        System.out.println(i);
	}
	public static void main(String[] args) {
		B b1 = new B(100);
	}
}
```

If in the parent class there is only constructors with arguments then as a programmer we should explicitly write super keyword in child class constructor
```java
package p1;
public class A {
	A(int i){
		System.out.println(i);
	}
}
```

```java
package p1;
public class B extends A {
	B(){
		System.out.println("B");
	}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```
-----
```java
package p1;
public class A {
	A(int i){
		System.out.println(i);
	}
}
```

```java
package p1;
public class B extends A {
	B(){
		super(500);
		System.out.println("B");
	}
	public static void main(String[] args) {
		B b1 = new B();
	}
}
```

Super keyword is not automatically get when there are only constructors with arguments in parent class. where as super keyword will be placed automatically when in the parent class there is a constructor with no arguments

```java
package p1;
public class A {
	A(int i){
		System.out.println(i);
	}
	A(){
		System.out.println("From Test");
	}
}
```

```java
package p1;
public class B extends A {
	B(){
		System.out.println("B");
	}
	public static void main(String[] args) {
		new B();
	}
}
```

We cannot us e this keyword and super keyword in the same constructor to calla
another constructor as ether of the statements becomes second statement then we will get an error

```java
package p1;
public class B extends A {
	B(){
		System.out.println("B");
	}
	B(int i){
		this(); super();
		System.out.println(i);
	}
	public static void main(String[] args) {
		new B();
		new B(100);
	}
}
```

If your child class constructor consist of thos keyword then in that constructor super keyword will not be automatically placed

```java
package p1;
public class A {
	A(int i){
		System.out.println(i);
	}
	A(){
		System.out.println("From A ");
	}
}
```

```java
package p1;
public class B extends A {
	B(){ //Super keyword is placed automatically
		System.out.println("B");
	}
	B(int i){ // super keyword is not placed automatically
		this();
		System.out.println(i);
	}
	public static void main(String[] args) {
		new B(100);
	}
}
```











