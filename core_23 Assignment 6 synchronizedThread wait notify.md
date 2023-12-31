### Synchronized thread ###

* When 2 threads are operating on common data the data might get corrupted because of Multitasking
* To make the threads operate one after another we use synchronized keyword where in the thread which has aquired the lock can only execute the block where as the other thread would be in wait status only when the 1st thread has releas the lock the other thread will get the opportunity to aquire the lock and execute the block

```java
public class A {
	int balance = 0;

	public static void main(String[] args) {
		A a1 = new A();
		a1.account();
		System.out.println(a1.balance);
	}

	public void account() {
		Thread t1 = new Thread(new Runnable() {

			@Override
			public void run() {
				add();
			}

		});

		Thread t2 = new Thread(new Runnable() {

			@Override
			public void run() {
				sub();
			}

		});
		t1.start();
		t2.start();
		try {
			t1.join();
			t2.join();
		} catch (Exception e) {
			System.out.println(e);
		}
		

	}

	public synchronized void add() {
		for (int i = 0; i < 10000; i++) {
			balance = balance + i;
		}
	}

	public synchronized void sub() {
		for (int i = 0; i < 10000; i++) {
			balance = balance - i;
		}
	}
}
```
----

### wait, notify ###

```java
public class A extends Thread {
	int total = 0;

	@Override
	public synchronized void run() {
		for (int i = 0; i < 1000; i++) {
			total = total + i;
		}
		notify();
	}
}
```

```java
public class B {
	public static void main(String[] args) {
		A a1 = new A();
		a1.start();

		synchronized (a1) {
			try {
				a1.wait();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}

		System.out.println(a1.total);
	}
}
```
