
# Packages in JAVA #

|                                 |  private |  default  | protected |  public  |
|---------------------------------|----------|-----------|-----------|----------|                      
|Same class                       |   Yes    |    Yes    |    Yes    |   Yes    |
|Same Package Sub Class           |   No     |    Yes    |    Yes    |   Yes    |
|Same Package non Sub Class       |   No     |    Yes    |    Yes    |   Yes    |
|Different Package Sub Class      |   No     |    No     |    Yes    |   Yes    |
|Different Package non Sub Class  |   No     |    No     |    No     |   Yes    |

## private ##
If you make a variable/method private then you cannot access that outside the class.

### Same class (private) ###
```java
package p1;

public class A {
	 private int x = 10;

	 private void test() {
		System.out.println("From Test");
	}
	 public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);
		a1.test();
	}
}
```

### Same package sub class (private) ###
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
package p1;

public class B extends A {
	
	public static void main(String[] args) {
		B b1 = new B();
		System.out.println(b1.x);//Error
		b1.test();//Error
	}
}
```

### Same package non sub class (private) ###

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
package p1;

public class B{
	
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.x);//Error
		a1.test();//Error
	}
}
```