**Create ER Diagram**

* open mySql workbench
* go to file , select new model
* select add diagram

**one to many maping**

![alt text](https://i.ibb.co/Jsz9mgV/image.png)

* now create a new database named `emp_db`

* we can create table by copying sql code from er diagram
* in the other hand we can create using entity class using hibernate
* create a new project
* create an entity package
* indside the package create a JPA Entity for class Country and add column name
* indside the package create a JPA Entity for class Employee 
* now go ro jpa design and select association

![alt text](https://i.ibb.co/CVSGbBf/image.png)

```java
@ManyToOne
    @JoinColumn(name = "country_id") //FK in the class it is mentioned
    private Country country;
```

* here Many refers to `employee` table and one refers to `country` table
* and JoinColumn `country_id` in which entity class it is present, it will automatically create column in entity class
* in foreign key table we have to write the mapping concepts on that table
* now create repository for both of the class
* create a controller layer and create addEmployee method

```java
@RestController
@RequestMapping("/api/v1/employees")
public class EmployeeController {

    private EmployeeRepository employeeRepository;

    public EmployeeController(EmployeeRepository employeeRepository) {
        this.employeeRepository = employeeRepository;
    }


    @PostMapping
    public ResponseEntity<Employee> addEmployee(@RequestBody Employee employee) {
        Employee savedEmp = employeeRepository.save(employee);
        return ResponseEntity.ok().body(savedEmp);
    }
}
```
* now run the application 
* if in our entity class has some other references variable present in it, in that case we have to supply entity obj with in the reference of the country object

```json
{
  "name": "John Doe",
  "addressLine": "123 Main Street",
  "country": {
    "id": 1,
    "countryName": "India"
  }
}

```

* The nested JSON structure reflects the relationship between the `Employee` and `Country` entities, where each employee is associated with a country. By embedding the country object within the employee JSON, it efficiently represents this relationship, making it clear that the country information is linked to each employee. This approach enhances data organization and comprehension, facilitating seamless communication between systems and users interacting with the API.

---
**another way**
```java
@RestController
@RequestMapping("/api/v1/employees")
public class EmployeeController {

    private EmployeeRepository employeeRepository;
    private CountryRepository countryRepository;

    public EmployeeController(EmployeeRepository employeeRepository, CountryRepository countryRepository) {
        this.employeeRepository = employeeRepository;
        this.countryRepository = countryRepository;
    }


    @PostMapping
    public ResponseEntity<Employee> addEmployee(@RequestParam long countryId, @RequestBody Employee employee) {
        Country country = countryRepository.findById(countryId).get();
        employee.setCountry(country);
        Employee savedEmp = employeeRepository.save(employee);
        return ResponseEntity.ok().body(savedEmp);
    }
}

```

![alt text](https://i.ibb.co/Gp0shxS/image.png)


**Many to many Mapping**

![alt text](https://i.ibb.co/QJ9T0jz/image.png)