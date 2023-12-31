```mermaid
graph LR
A((New)) -- Start --> B(1 2 3 4 5 6 7 runnable)
B --> C((running))
C -- Thread Scheduled -->B
C --> D[terminated]
B --> E((sleep))
E --> C
B --> F((wait))
F -- notify, notify all--> C

```

```java
public class A extends Thread {
	public static void main(String[] args) {
		A a1 = new A();
		System.out.println(a1.getState());
		a1.start();

		try {
			Thread.sleep(5000);
		} catch (Exception e) {
			e.printStackTrace();
		}
		System.out.println(a1.getState());
	}

	@Override
	public void run() {
		System.out.println("Test");
	}
}

```