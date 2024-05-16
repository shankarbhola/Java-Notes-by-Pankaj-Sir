**deleteById( )**

```java
//Test
@Test
	void deleteEmployee() {
		employeeRepository.deleteById(2);
	}
```
**findById( )**
```java
//Test
@Test
	void fetchEmployee() {
		Optional<Employee> byId = employeeRepository.findById(4);
		Employee employee = byId.get();
		System.out.println(employee.getId());
		System.out.println(employee.getName());
		System.out.println(employee.getEmail());
		System.out.println(employee.getSalary());
	}
```
findById() returns optional type
to convert optional type to Employee object type use get() method.

**findAll()**
```java
//Test
@Test
void fetchAllEmployeeDetails() {
    Iterable<Employee> data = employeeRepository.findAll();
    for (Employee employee : data) {
        System.out.println(employee.getId());
        System.out.println(employee.getName());
        System.out.println(employee.getEmail());
        System.out.println(employee.getSalary());
    }
}
```

**for custom query**
go to repository 
Method name should starts with findBy
 ```findByColumnname(String Columnname)```

```java
//EMployeeRepository.java
package com.demo.repository;

import org.springframework.data.repository.CrudRepository;

import com.demo.entity.Employee;

public interface EmployeeRepository extends CrudRepository<Employee, Integer> {
	Employee findByEmail(String email);
}

```
```java
//Test
@Test
	void fetchByEmail() {
		Employee employee = employeeRepository.findByEmail("kunal@gmail.com");
		System.out.println(employee.getId());
		System.out.println(employee.getName());
		System.out.println(employee.getEmail());
		System.out.println(employee.getSalary());
	}
```
---
FindBySalary
```java
//EmployeeRepository.java
public interface EmployeeRepository extends CrudRepository<Employee, Integer> {
	Employee findByEmail(String email);
	Iterable<Employee> findBySalary(int salary);
}
```
```java
//Test
@Test
	void fetchAllEmployeeBySalary() {
		Iterable<Employee> data = employeeRepository.findBySalary(5000);
		for (Employee employee : data) {
			System.out.println(employee.getId());
			System.out.println(employee.getName());
			System.out.println(employee.getEmail());
			System.out.println(employee.getSalary());
		}
	}
```

**findByEmailAndSalary(String Email, int Salary)**
```java
//EmployeeRepository.java
public interface EmployeeRepository extends CrudRepository<Employee, Integer> {
	Employee findByEmail(String email);
	Iterable<Employee> findBySalary(int salary);
	Employee findByEmailAndSalary(String email, int salary);
}
```
```java
//Test
@Test
	void fetchEmployeeByEmailAndSalary() {
		Employee employee = employeeRepository.findByEmailAndSalary("mike@gmail.com", 7000);
		System.out.println(employee.getId());
		System.out.println(employee.getName());
		System.out.println(employee.getEmail());
		System.out.println(employee.getSalary());
	}
```
**findByEmailOrSalary(String Email, int Salary)**
```java
//EmployeeRepository.java
Iterable<Employee> findByEmailOrSalary(String email, int salary);
```
```java
//Test
@Test
	void fetchEmployeeByEmailOrSalary() {
		Iterable<Employee> data = employeeRepository.findByEmailOrSalary("mike@gmail.com", 5000);
		for (Employee employee : data) {
			System.out.println(employee.getId());
			System.out.println(employee.getName());
			System.out.println(employee.getEmail());
			System.out.println(employee.getSalary());
		}
	}
```
**@Query annotation**
This is JPQL (Java Persistence Query Language)
@Query is used to develop custom query
```java
//EmployeeRepository.java
public interface EmployeeRepository extends CrudRepository<Employee, Integer> {
	Employee findByEmail(String email);
	Iterable<Employee> findBySalary(int salary);
	Employee findByEmailAndSalary(String email, int salary);
	Iterable<Employee> findByEmailOrSalary(String email, int salary);
	
	 @Query("SELECT e FROM Employee e WHERE e.email = :email")
	 Employee searchByEmail(String email);
}
```
```java
//Test
@Test
void searchByEmail() {
    Employee employee = employeeRepository.searchByEmail("kunal@gmail.com");
    System.out.println(employee.getId());
    System.out.println(employee.getName());
    System.out.println(employee.getEmail());
    System.out.println(employee.getSalary());
}
```
---

```java
//EmployeeRepository.java
public interface EmployeeRepository extends CrudRepository<Employee, Integer> {
	Employee findByEmail(String email);
	Iterable<Employee> findBySalary(int salary);
	Employee findByEmailAndSalary(String email, int salary);
	Iterable<Employee> findByEmailOrSalary(String email, int salary);
	
	 @Query("SELECT e FROM Employee e WHERE e.email = :email")
	 Employee searchByEmail(String email);
	 
	 @Query("SELECT e FROM Employee e WHERE e.email = ?1 OR e.salary = ?2")
	 Iterable<Employee> searchByEmailOrSalary(String email, int salary);
}

```
```java
//Test
@Test
	void fetchEmployeeByEmailOrSalary() {
		Iterable<Employee> data = employeeRepository.searchByEmailOrSalary("mike@gmail.com", 5000);
		for (Employee employee : data) {
			System.out.println(employee.getId());
			System.out.println(employee.getName());
			System.out.println(employee.getEmail());
			System.out.println(employee.getSalary());
		}
	}
```