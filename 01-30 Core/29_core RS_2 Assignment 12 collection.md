reading the data from an array list based on index number using get method
```java
System.out.println(x.get(1));
```
---
```java
Iterator itr = x.iterator();
		while(itr.hasNext()) {
			System.out.println("Value of x:"+itr.next());
		}
```	

![picture](https://i.ibb.co/bQ43B29/image.png)
In jdk linkedlist is internaly implemented as doubly linkedlist
```java
package app_java_1;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;

public class A {
	

	public static void main(String[] args) {
		List<Integer> x = new LinkedList<Integer>();

		x.add(10);
		x.add(20);
		x.add(30);
		System.out.println("Array size : "+x.size());
		System.out.println("add method():"+x);
		
		x.add(1, 500);
		System.out.println("add(index, value) method():"+x);
		
		List<Integer> y = new LinkedList<Integer>();
		y.add(300);
		y.add(500);
		
		x.addAll(2,y);
		System.out.println("addAll(index, collection) method():"+x);
		
		if (x.contains(500)) {
			System.out.println("Yes Present");
		} else {
			System.out.println("No Present");
		}
		
		x.remove(1);
		System.out.println("remove(index) method():"+x);
		
		System.out.println(x.get(1));
		
		Iterator itr = x.iterator();
		while(itr.hasNext()) {
			System.out.println("Value of x:"+itr.next());
		}
	}
}

```
---
```java
package app_java_1;

import java.util.LinkedList;

public class B {
	public static void main(String[] args) {
		LinkedList<Integer> x = new LinkedList<Integer>();
		x.add(100);
		x.add(200);
		x.add(300);
		x.add(400);
		x.addFirst(500);
		x.addLast(700);
		x.addFirst(50000);
		x.addLast(70);
		x.add(450);
		System.out.println(x);
	}
}

```
---
```java
package p1;

public class Employee {
	private String firstname;
	private String lastname;
	private int id;
	
	Employee(String firstname, String lastname, int id) {
		this.firstname = firstname;
		this.lastname = lastname;
		this.id = id;
	}
	
	public String getFirstname() {
		return firstname;
	}
	public void setFirstname(String firstname) {
		this.firstname = firstname;
	}
	public String getLastname() {
		return lastname;
	}
	public void setLastname(String lastname) {
		this.lastname = lastname;
	}
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
}
```

```java
package p1;

import java.util.LinkedList;

public class A {
	public static void main(String[] args) {
		Employee arun = new Employee("arun", "k", 100);
		Employee ravi = new Employee("ravi", "kiran", 200);
		Employee santosh = new Employee("santosh", "m", 300);
		
		LinkedList<Employee> empDetails = new LinkedList<Employee>();
		empDetails.add(arun);
		empDetails.add(ravi);
		empDetails.add(santosh);
		
		System.out.println(empDetails);
		
		for (Employee employee : empDetails) {
			System.out.println(employee.getFirstname());
			System.out.println(employee.getLastname());
			System.out.println(employee.getId());
		}
	}
}

```