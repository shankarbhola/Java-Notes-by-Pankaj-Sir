## this keyword in java ##
* this keyword is special reference variable that automatically gets created to store object's address.

```java
package p1;
public class A {
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1);
		a1.test();
	}

	public void test() {
		System.out.println(this);
	}
	
}
```
---
```java
package p1;
public class A {
	int X = 10;
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.X);
		a1.test();
	}
	public void test() {
		System.out.println(this.X);
	}
	
}
```

* We cannot use this keyword inside static method
```java
package p1;
public class A {
	int X = 10;
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(this);
	}
	public static void test() {
		System.out.println(this);
	}
	
}
```
---
```java
package p1;

public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test1();
	}

	public void test1() {
		this.test2();
	}

	public void test2() {
		System.out.println("From test2");
	}
}
```
---
```java
package p1;

public class A {
	static int x= 10;
	public static void main(String[] args) {
		A a1 = new A();
		a1.test1();
	}

	public void test1() {
		System.out.println(this.x);
		//the static field A.x should be accessable in a static way
	}
}
```

* this keyword will automaticallyhold the current objects address that is running in our progeam

```java
package p1;

public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test1();
		A a2 = new A();
		a2.test1();
        a1.test1();
        a2.test1();
        a2.test1();
	}

	public void test1() {
		System.out.println(this);
	}
}
```