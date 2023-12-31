####Different Package Sub class (private)

```java
package p1;

public class A {
	private int x = 10;

	private void test() {
		System.out.println("From Test");
	}
}
```

```java
package p2;

import p1.A;

public class C extends A{
	public static void main(String[] args) {
		C c1 = new C();
		System.out.println(c1.x); //Error
		c1.test(); //Error
	}
}
```


####Different Package non Sub class (private)

```java
package p1;

public class A {
	private int x = 10;

	private void test() {
		System.out.println("From Test");
	}
}
```
```java
package p2;

import p1.A;

public class C {
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);//Error
		a1.test();//Error
	}
}
```


##Default

####Same class

```java
 package p1;

public class A {
	 int x = 10;

	 void test() {
		System.out.println("From Test");
	}
	 public static void main(String[] args) {
		 A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}
```

####Same Package sub class (default)

```java
package p1;

public class A {
	 int x = 10;

	 void test() {
		System.out.println("From Test");
	}
	 
}
```

```java
package p1;

public class B extends A {
	
	public static void main(String[] args) {
		B b1 = new B();
		System.out.println(b1.x);
		b1.test();
	}
}
```

####Same PAckage non sub class (default)

```java
package p1;

public class A {
	 int x = 10;

	 void test() {
		System.out.println("From Test");
	}
}
```

```java
package p1;

public class B {
	
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}
```

####Different Package Sub class (default)
---------------------------
```java
package p1;

public class A {
	 int x = 10;

	 void test() {
		System.out.println("From Test");
	}
	 
}
```
```java
package p2;

import p1.A;

public class C extends A {
	
	public static void main(String[] args) {
		C c1 = new C();
		System.out.println(c1.x); //Error
		c1.test(); //Error
	}
}
```

####Different Package non Sub class (default)

```java
package p1;

public class A {
	 int x = 10;

	 void test() {
		System.out.println("From Test");
	}
	 
}
```

```java
package p2;

import p1.A;

public class C {
	
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}

```

##Protected
####Same class (protected)

```java
package p1;

public class A {
	 protected int x = 10;

	 protected void test() {
		System.out.println("From Test");
	}
	 public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}
```

####Same package sub class (protected)

```java
package p1;

public class A {
	 protected int x = 10;

	 protected void test() {
		System.out.println("From Test");
	}
	 
}
```
```java
package p1;

public class B extends A {
	
	public static void main(String[] args) {
		B b1 = new B();
		System.out.println(b1.x);
		b1.test();
	}
}
```

####Same package non sub class (protected)

```java
package p1;

public class A {
	 protected int x = 10;

	 protected void test() {
		System.out.println("From Test");
	}
	 
}
```

```java
package p1;

public class B{
	
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}
```


####Different Package Sub class (protected)

```java
package p1;

public class A {
	 protected int x = 10;

	 protected void test() {
		System.out.println("From Test");
	}
	 
}
```

```java
package p2;

import p1.A;

public class C extends A{
	
	public static void main(String[] args) {
		C c1 = new C();
		System.out.println(c1.x);
		c1.test();
	}
}
```

####Different Package non sub class (protected)

```java
package p1;

public class A {
	 protected int x = 10;

	 protected void test() {
		System.out.println("From Test");
	}
	 
}
```

```java
package p2;

import p1.A;

public class C{
	
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x); //Error
		a1.test(); //Error
	}
}
```