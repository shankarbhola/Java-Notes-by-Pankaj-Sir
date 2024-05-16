```java
public class A {
    public static void main(String[] args) {
        List<String> data = Arrays.asList("mike", "stallen", "adam");
        List<String> newData = data.stream().map(str -> str.toUpperCase()).collect(Collectors.toList());
        System.out.println(newData);

    }
}
```

```java
OUTPUT
[MIKE, STALLEN, ADAM]
```
---
```java
public class A {
    public static void main(String[] args) {
        List<Integer> data = Arrays.asList(10,3,4);
        List<Integer> newData = data.stream().map(N -> N*5).collect(Collectors.toList());
        System.out.println(newData);

    }
}
```

```java
OUTPUT
[50, 15, 20]
```

**Consumer functional interface**
```java
//Consumer functional interface will take one input will not produce any output
public class A {
    public static void main(String[] args) {
        Consumer<Integer> c = (x) -> System.out.println(x);
        c.accept(100);
    }
}
```
```java
OUTPUT
100
```
---
```java
public class A {
    public static void main(String[] args) {
        List<String> data = Arrays.asList("mike", "smith", "adam", "madam", "mike");
        data.forEach(s -> System.out.println(s));
    }
}
```
```java
OUTPUT
mike
smith
adam
madam
mike
```
**Supplier functional interface**

```java
public class A {
    public static void main(String[] args) {
        Supplier<Double> val = () -> Math.random();
        System.out.println(val.get());
    }
}
```
```java
OUTPUT
0.8560912963261247
```
**Stream**
Sorting
```java
public class A {
    public static void main(String[] args) {
        List<Integer> data = Arrays.asList(10, 2, 15, 20, 25);
        List<Integer> newData = data.stream().sorted().collect(Collectors.toList());
        System.out.println(newData);
    }
}
```
```java
OUTPUT
[2, 10, 15, 20, 25]
```
---
```java
public class A {
    public static void main(String[] args) {
        List<String> data = Arrays.asList("mike", "smith", "adam", "madam");
        List<String> newData = data.stream().sorted().collect(Collectors.toList());
        System.out.println(newData);
    }
}
```
```java
OUTPUT
[adam, madam, mike, smith]
```
---
```java
public class A {
    public static void main(String[] args) {
        List<String> data = Arrays.asList("mike", "smith", "adam", "madam", "mike");
        List<String> newData = data.stream().distinct().collect(Collectors.toList());
        System.out.println(newData);
    }
}
```
```java
OUTPUT
[mike, smith, adam, madam]
```
