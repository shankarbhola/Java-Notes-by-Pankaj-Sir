**@SuppressWarning**
```java
public class A{
	public static void main(String[] args) {
		
		@SuppressWarnings("unused")
		int i = 10;
		int j = 100; //warning
		int k = 300; //Warning
	}
}
```
```java
public class A{
	@SuppressWarnings("unused")
	public static void main(String[] args) {
		
		int i = 10;
		int j = 100;
		int k = 300;
	}
}
```

**@Deprecated**
![picture](https://i.ibb.co/x2GHQ6p/1.jpg)
![picture](https://i.ibb.co/gvLLbkb/1.png)
```java
public class A{
	public static void main(String[] args) {
		A a1 = new A();
		a1.findById();
	}
	@Deprecated
	public void findById() {
		
	}
	public void searchById() {
		
	}
}
```

