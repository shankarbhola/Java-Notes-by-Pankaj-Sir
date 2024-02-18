### Return ###
* We can use "return" keyword insite void methods only
* it is optional to use
* It will return control to method calling statement

```java
public class A {
	public static void main(String[] args) {
		A a1 = new A();
	}
	public void test() {
		System.out.println("From test");
		return;
	}
}
```

----


```java
public class A {
	public static void main(String[] args) {
		System.out.println("Welcome");
        return;
	}
}
```

----

```java
public class A {
	public static void main(String[] args) {
		System.out.println("Welcome");
		return;
		System.out.println(100); //Error
	}
}
```

* If we write only code after return keyword we will  get unrechable Error.

### return value ###
* We can use return value keyword only inside not a void method & it is mandatory to be used.

```java
class A{
    psvm(){
        publuc int test(){ //Error

        }
    }
}
```

* return value keyword wil return control and value to method calling statement.

```java
class A{
    psvm(){

    }
    public int test(){
        return 100;
        sop(200); //unreachable code error
    }
}
```

## Method arguments ##
```java
class A{
    psvm(){
        A a1 = new A();
        a1.test();
    }
    public void test(int x){ //method argu,ents(local variable) 
    sop(x);

    }
}
```
---
```java
public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test(100, "mike");
	}
	public void test(int x, String y) {
		System.out.println(x);
		System.out.println(y);
	}
}
```

---
```java
public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test(100, 200,300);
	}
	public void test(int... x) {
		System.out.println(x[0]);
		System.out.println(x[1]);
		System.out.println(x[2]);
	}
}
```

---
```java
public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test1();
	}
	public void test1() {
		A a2 = new A();
		a2.test2();
	}
	public void test2() {
		System.out.println("From test2");
	}
}
```

 ---
```java
 public class A {
	public static void main(String[] args) {
		A a1 = new A();
		a1.test1();
		a1.test1();
		a1.test1();
	}
	public void test1() {
	System.out.println(100);
	}		
}
```

---

```java
public class A {
	public static void main(String[] args) {
	A.test1();
	}
	public static void test1() {
	A a1 = new A();
	a1.test2();
	}
	public void test2() {
		System.out.println(100);
	}
}

```