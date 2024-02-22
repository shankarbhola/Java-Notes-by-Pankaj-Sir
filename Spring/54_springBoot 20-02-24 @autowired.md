![](https://i.ibb.co/2kd0H38/image.png)

![](https://i.ibb.co/zGY9bq7/image.png)


### @Singleton ###
Here we design the class such that only one object of the class at most can be created.
* to design a singleton class make the constructor private.
* make the reference variable private
```java
package p1;

public class A {
	static A a1 = null;
	
	private A(){
		
	}
	
	public static A getInstance() {
		if (a1==null) {
			a1=new A();
		}
		return a1;
	}
}
```

```java
package p1;

public class B {
	public static void main(String[] args) {
		A a1 = A.getInstance();
		A a2 = A.getInstance();
		System.out.println(a1);
		System.out.println(a2);
 	}
}

```