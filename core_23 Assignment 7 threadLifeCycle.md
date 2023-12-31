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
```
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