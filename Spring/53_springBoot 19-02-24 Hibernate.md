
Create new Spring starter project

![picture](https://i.ibb.co/QnTHT0x/image.png)

click next

![picture](https://i.ibb.co/qxw7RC4/image.png)

select mysql driver
then search jpa for hibernate

![](https://i.ibb.co/2jB64Pc/image.png)

click finish

Open src/main/resources
then open application.properties file

For connecting to the database
```properties [application.properties]
#application.properties

spring.datasource.url=jdbc:mysql://localhost:3306/demo-2
spring.datasource.username=root
spring.datasource.password=system

#Create table
#spring.jpa.hibernate.ddl-auto=create

#Update table
spring.jpa.hibernate.ddl-auto=update

spring.jpa.show-sql=true
```

---

* go to src/main/java
* Create a new package named ```com.demo.entity```
* Inside ```com.demo.entity``` create a class ```Employee```

```java
package com.demo.entity;

import jakarta.persistence.*;

@Entity
public class Employee {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private int id;
	private String name;
	private String email;
	private int salary;
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public int getSalary() {
		return salary;
	}
	public void setSalary(int salary) {
		this.salary = salary;
	}
}

```