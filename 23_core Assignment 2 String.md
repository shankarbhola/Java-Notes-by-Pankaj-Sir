### Mutable ###
Mutable is something where the class object properties keeps on changing

### Immutable ###
Immutable class once its object is created then its state cannot be altered.

Steps to create Immutable class: 
* Create a final class
* Set the values of the properties using onlu constructors
* Make the properties as final
* Do not provide any setters for these properties

```java
final public class A {
	private final int age;
	private final String name;

	public A(int age, String name) {
		this.age = age;
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public String getName() {
		return name;
	}

	public static void main(String[] args) {
		A a1 = new A(20, "Pankaj");
		System.out.println(a1.getAge());
		System.out.println(a1.getName());
	}
}
```

---
```java
final public class A {
	public static void main(String[] args) {
		String s1 = new String("xyz");
		String s2 = new String("xyz");
		System.out.println(s1==s2);
		System.out.println(s1.equals(s2));
	}
}
```
```mermaid
graph LR
A(String s1 = ''pankaj'')
B(String s2 = ''Pankaj'')
C((Object))
A -->C
B --> C
```

```mermaid
graph LR
A(String s3 = ''xyz'')
B(String s4 = ''xyz'')
C((Object))
A -->C
B --> C
```
```mermaid
graph LR
A(s1 == s2) --> B[true]
C(s3 == s4) --> B
```

s1.equals(s2) --> true
s3.equals(s4) --> true

---
String s1 = new String ("xyz");

```mermaid
graph LR
A(S1)-->B((Object 1))
```

```mermaid
graph LR
A(String s2 = ''xyz'')
B(String s3 = ''xyz'')
C((Object 2))
A -->C
B --> C
```

String s4 = new String ("xyz");
```mermaid
graph LR
A(s4)-->B((Object 3))

C(s1 == s4)-->D[false]
E(s2 == s1)-->D
F(s2 == s3) --> G[true]
```
---
A(String s1 = ''xyz'');
```mermaid
graph LR
A(s1)-->B((xyz))-->C[garbage collector]
```
s1 = "abc";

```mermaid
graph LR
A(s1)--xB((xyz))-->C[garbage collector]
A(s1)-->D((abc))
```
s1 = "xxxx"
```mermaid
graph LR
A(s1)--xB((xyz))-->C[garbage collector]
A(s1)--xD((abc))-->E[garbage collector]
A(s1)-->F((xxxx))
```
---


```mermaid
graph LR
A(String s1 = ''xyz'')
B(String s2 = ''xyz'')
C((xyz))
A -->C
B --> C
```

```mermaid
graph LR
A(String s3 = ''abc'')
B(String s4 = ''abc'')
C((abc))
A -->C
B --> C
```