```java
public class A {
	public static void main(String[] args) {
		Predicate<String> val = x->x.startsWith("s");
		boolean result = val.test("stallen");
		System.out.println(result);
	}
}
```
**Stream**
Printing even numbers
```java
public class A {
	public static void main(String[] args) {
		List<Integer> data = Arrays.asList(10,20,25,12,23);
		List<Integer> newData = data.stream().filter(x->x%2==0).collect(Collectors.toList());
		System.out.println(newData);
	}
}
```
![](https://i.ibb.co/ScG5Xzk/image.png)
```java
OUTPUT
[10, 20, 12]
```

Printing odd numbers
```java
public class A {
	public static void main(String[] args) {
		List<Integer> data = Arrays.asList(10,20,25,12,23);
		List<Integer> newData = data.stream().filter(i->i%2!=0).collect(Collectors.toList());
		System.out.println(newData);
	}
}
```
![](https://i.ibb.co/cYp8B9n/image.png)
```java
OUTPUT
[25, 23]
```
**String filter**
```java
public class A {
	public static void main(String[] args) {
		List<String> data = Arrays.asList("mike", "stallin", "madam", "jhon");
		List<String> newData = data.stream().filter(s->s.startsWith("m")).collect(Collectors.toList());
		System.out.println(newData);
	}
}
```
![](https://i.ibb.co/TYdxCQY/image.png)
```java
OUTPUT
[mike, madam]
```

**Function Functional Interface**
```java
//Function Functional Interface - it takes one input and produces an output
public class A {
	public static void main(String[] args) {
		Function<Integer,Integer> val = x->x*x;
		Integer result = val.apply(10);
		System.out.println(result);
	}
}
```
---

```java
public class A {
	public static void main(String[] args) {
		Function<Integer,String> val = x->"Output is:"+x;
		String result = val.apply(10);
		System.out.println(result);
	}
}
```
---

```java
public class A {
	public static void main(String[] args) {
		List<Integer> data = Arrays.asList(10,12,34,5,6);
		List<Integer> newData = data.stream().map(x->x*x).collect(Collectors.toList());
		System.out.println(newData);
	}
}
```