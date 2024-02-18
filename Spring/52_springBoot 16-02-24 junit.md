All dependencies are stored at C:\Users\user_name\ .m2

Sometimes all project files are not downloaded correctly and it shows error, Top fix this right click on your project > go to maven > click on Update Project

![picture](https://i.ibb.co/txgXHK8/image.png)

If not working Close STS then delete .m2 folder then reopen STS again and create a new project

---
**What is Starter Dependencies?**
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter</artifactId>
</dependency>
```
In Spring Boot, starter dependencies are a convenient way to manage dependencies for common tasks or features in your application. Spring Boot provides a wide range of starter dependencies that you can include in your project's pom.xml file to quickly set up various functionalities without having to manually manage individual dependencies.

Starter dependencies are the one that helps us to download pair minimum library require to begin the project

### JUnit ###
**@Test**
@Test annotation is used in JUnit to chek whether every code in that method is running or not. If not it will report a filure and if the method runs properly it will repost passed.

![picture](https://i.ibb.co/MpBKQ3H/image.png)
![picture](https://i.ibb.co/DGt8gfY/image.png)

To run only particular method, select the method then run with junit 

![picture](https://i.ibb.co/LzjdRzS/image.png)


**@BeforeEach**
@BeforeEach is used to signal that the annotated method should be executed before each @Test
```java
package com.demo;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class Demo1ApplicationTests {

	@Test
	void test1() {
		System.out.println("From test1");
	}
	
	@Test
	void test2() {
		System.out.println("From test2");
	}
	
	@BeforeEach
	void beforeMethod() {
		System.out.println("Before Method");
	}
}
```
```java
OUTPUT
Before Method
From test1
Before Method
From test2
```

**@AfterEach**
@AfterEach is used to signal that the annotated method should be executed after each @Test
```java
package com.demo;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class Demo1ApplicationTests {

	@Test
	void test1() {
		System.out.println("From test1");
	}
	
	@Test
	void test2() {
		System.out.println("From test2");
	}
	
	@BeforeEach
	void beforeMethod() {
		System.out.println("Before Method");
	}
	
	@AfterEach
	void aftreMethod() {
		System.out.println("After Method");
	}
}
```
```java
OUTPUT
Before Method
From test1
After Method
Before Method
From test2
After Method
```
**@BeforeAll**
@BeforeAll is used to signal that the annotated method should beexecuted before all tests in the current test class. 
```java
package com.demo;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class Demo1ApplicationTests {

	@Test
	void test1() {
		System.out.println("From test1");
	}
	
	@Test
	void test2() {
		System.out.println("From test2");
	}
	
	@BeforeEach
	void beforeMethod() {
		System.out.println("Before Method");
	}
	
	@AfterEach
	void aftreMethod() {
		System.out.println("After Method");
	}
	
	@BeforeAll
	static void beforeAllMethod() {
		System.out.println("Before");
	}
	
}
```
```java
OUTPUT
Before
Before Method
From test1
After Method
Before Method
From test2
After Method
```

**@AfterAll**
@AfterAll is used to signal that the annotated method should beexecuted after all tests in the current test class. 
```java
package com.demo;

import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class Demo1ApplicationTests {

	@Test
	void test1() {
		System.out.println("From test1");
	}
	
	@Test
	void test2() {
		System.out.println("From test2");
	}
	
	@BeforeEach
	void beforeMethod() {
		System.out.println("Before Method");
	}
	
	@AfterEach
	void aftreMethod() {
		System.out.println("After Method");
	}
	
	@BeforeAll
	static void beforeAllMethod() {
		System.out.println("Before");
	}
	
	@AfterAll
	static void afterAllMethod() {
		System.out.println("After");
	}
	
}
```
```java
OUTPUT
Before
Before Method
From test1
After Method
Before Method
From test2
After Method
After
```