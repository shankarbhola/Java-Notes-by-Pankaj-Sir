Threads 
------
* Multitasking done at the program level is called as Threads
* The main purpose of threads is improve the performance of the application by reducing execution time

```java
public class A extends Thread{ //run() , start()
	
	@Override
	public void run() {
		for (int i = 0; i < 10000; i++) {
			System.out.println("run");
		}
	}
	public static void main(String[] args) {
		A a1 = new A();
		a1.start();
		for (int i = 0; i < 10000; i++) {
			System.out.println("Main");
		}
	}
}
```
---
```java
public class A extends Thread{ //run() , start()
	String name;
	A(String name){
		this.name = name;
	}
	@Override
	public void run() {
		for (int i = 0; i < 10000; i++) {
			System.out.println(this.name);
		}
	}
}
```

```java
public class B {
    public static void main(String[] args) {
    	A a1 = new A("xxx");
    	A a2 = new A("yyy");
    	A a3 = new A("zzz");
    	
    	a1.start();
    	a2.start();
    	a3.start();
    }
}
```
---

```java
public class A implements Runnable{
	String name;
	A(String name){
		this.name = name;
	}
	@Override
	public void run() {
		for (int i = 0; i < 10000; i++) {
			System.out.println(this.name);
		}
	}
	
	public static void main(String[] args) {
		A a1 = new A("xxx");
		Thread t1 = new Thread(a1);
		t1.start();
		
		A a2 = new A("yyy");
		Thread t2 = new Thread(a2);
		t2.start();
		
		for (int i = 0; i < 10000; i++) {
			System.out.println("main");
		}
	}
}
```
