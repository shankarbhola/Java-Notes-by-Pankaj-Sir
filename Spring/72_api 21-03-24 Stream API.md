```java
//Employee.java
package org.example;

public class Employee {
    private long id;
    private String name;
    private int salary;

    //constructor with arguments
    public Employee(long id, String name, int salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    //getters for all properties
    public long getId() {
        return id;
    }
    public String getName() {
        return name;
    }
    public int getSalary() {
        return salary;
    }
}
```
```java
//A.java
package org.example;

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class A {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
                new Employee(1, "abc", 5000),
                new Employee(2, "def", 6000),
                new Employee(3, "ghi", 7000)
        );
        List<Employee> newData = employees.stream().filter(e -> e.getSalary() > 5000).collect(Collectors.toList());
        for (Employee employee : newData) {
            System.out.println(employee.getId());
            System.out.println(employee.getName());
            System.out.println(employee.getSalary());
        }
    }

}
```
```java
List<Employee> newData = employees.stream().filter(e->e.getName().equals("abc")).collect(Collectors.toList());
```