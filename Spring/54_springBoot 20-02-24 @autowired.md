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

![](https://i.ibb.co/QvCB54C/image.png)

* To create repository go to ```src/main.java```
* create a new package ```com.demo.repository```

```java
//EmployeeRepository.java
package com.demo.repository;

import org.springframework.data.repository.CrudRepository;

import com.demo.entity.Employee;

public interface EmployeeRepository extends CrudRepository<Employee, Integer> {

}
```

```java
//src/test/java
package com.demo;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import com.demo.entity.Employee;
import com.demo.repository.EmployeeRepository;

@SpringBootTest
class Demo2ApplicationTests {
	
	@Autowired
	private EmployeeRepository employeeRepository;

	@Test
	void SaveEmployeeDetails() {
		Employee e = new Employee();
		e.setName("Amit");
		e.setEmail("amit@gmail.com");
		e.setSalary(5000);
		
		employeeRepository.save(e);
	}

}
```