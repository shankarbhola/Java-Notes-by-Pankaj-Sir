##public
####Same class (public)

```java
package p1;

public class A {
	 public int x = 10;

	 public void test() {
		System.out.println("From Test");
	}
	 public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}
```

####Same package sub class (public)

```java
package p1;

public class A {
	 public int x = 10;

	 public void test() {
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

####Same package non sub class (public)

```java
package p1;

public class A {
	 public int x = 10;

	 public void test() {
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

####Different Package Sub class (public)

```java
package p1;

public class A {
	 public int x = 10;

	 public void test() {
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

####Different Package non sub class (public)
```java

package p1;

public class A {
	 public int x = 10;

	 public void test() {
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
		System.out.println(a1.x);
		a1.test(); 
	}
}
```

##Classes with access specifier

* A class cannot be private / protected
* A class can be only public & default
* A default class can be accessed only inside same package

```java
package p1;
class A {
	 
}
```

```java
package p1;
public class B extends A {
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p2;
import p1.A;
public class C extends A{
	public static void main(String[] args) {
		A a1 = new A(); //Error
	}
}
```

* A public class can be accessed in same or Different 
```java
Packages
package p1;
public class A {
	 
}
```

```java
package p1;
public class B extends A {
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

```java
package p2;
import p1.A;
public class C extends A{
	public static void main(String[] args) {
		A a1 = new A();
	}
}
```

##Constructor with access specifier

* If a Constructor is made private then it's object cannot be created in Different class

```java
package p1;
public class A{
    private A() {
		 
	 }
	public static void main(String[] args) {
        A a1 = new A(); //Correct		
	}
}
```

```java
package p1;
public class B {
	public static void main(String[] args) {
		A a1 = new A(); //Error
	}
}
```

```java
package p2;
import p1.A;
public class C{
	public static void main(String[] args) {
		A a1 = new A(); //Error
	}
}
```

* Constructors are not inherited.
* In a class if a Constructor is private then that class is not eligible for inheritance

```java
package p1;
public class A{
    private A() {
		 
	 }
	public static void main(String[] args) {
        		
	}
}
```

```java
package p1;
public class B extends A{ //Error
	public static void main(String[] args) {
		
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