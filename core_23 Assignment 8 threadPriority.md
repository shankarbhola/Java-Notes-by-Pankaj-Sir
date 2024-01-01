### Thread Priority ###
* It decides thread priority is going to run first and which thread will run later
* If we set the priority then it is a request made to the thread scheduler where there is no assurity that it will be process and approve
* The minimun thread priority is 1 , maximum thread priority is 10 and the normal thread priority is 5 however we can set the thread priority with the number anything between 1 to 10

```java
public class A extends Thread {
	String name;
	A(String name){
		this.name = name;
	}
	public static void main(String[] args) {
		A a1 = new A("xxxx");
		A a2 = new A("yyyy");
		a2.setPriority(10);
		a1.setPriority(1);
		System.out.println(a1.getPriority());
		System.out.println(a2.getPriority());
		a1.start();
		a2.start();
	}
	
	@Override
	public void run() {
		System.out.println(this.name);
	}
}
```
---
### setting a name and getting a name of thread 
```java
public class A extends Thread {
	String name;
	A(String name){
		this.name = name;
	}
	public static void main(String[] args) {
		A a1 = new A("xxxx");
		A a2 = new A("yyyy");
		a1.setName("addAmount");
		a2.setName("withdrawAmount");
		System.out.println(a1.getName());
		System.out.println(a2.getName());
		a1.start();
		a2.start();
	}
	
	@Override
	public void run() {
		System.out.println(this.name);
	}
}

```