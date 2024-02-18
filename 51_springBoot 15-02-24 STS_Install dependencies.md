## STS Installation ##
* Download STS [spring.io/tools](https://spring.io/tools)
* Download Windows X86_64
* Double click to extract the jar file
* open extracted file the run SpringToolSuite4.exe application file

Create Project using Spring Initializer
* go to [start.spring.io](https://start.spring.io/)

![picture](https://i.ibb.co/py5xV5t/image.png)

Create project using STS
* Click on the File menu -> New -> Spring stater project
![picture](https://i.ibb.co/BNn0hhq/image.png)

### Maven ### 
Maven is a build automation tool used primarily for Java projects. It simplifies the process of managing dependencies, building, testing, and deploying Java applications. Maven uses a project object model (POM) file to describe the project configuration and dependencies.

**pom.xml:** In a Maven project, the pom.xml (Project Object Model) file is used to define the project configuration, including its dependencies. Dependencies in the pom.xml file specify external libraries or modules that your project relies on to compile, build, and run successfully.

**Dependency:** Maven manages project dependencies by retrieving them from repositories, which can be local or remote. It automatically downloads necessary libraries and plugins required for the project.
[mvnrepository.com](https://mvnrepository.com/) is a popular website that serves as a repository for Maven artifacts. It provides a user-friendly interface for searching and browsing Java libraries and dependencies that are available in the Maven Central Repository.

For add mysql connector jar file add this to under dependencies tag inside pom.xml 
```xml
<!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.0.33</version>
</dependency>
```


