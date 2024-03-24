IntelliJ IDEA Installation
-
* go to [jetbrains.com](https://www.jetbrains.com/idea/download/?section=windows) website and download community edition
* Install it
* in community edition directly creating spring boot project i intellij plugin is not available , it is available in ultimate version which is a paid version
* go to spring initializer website and create a spring boot project
![alt text](https://i.ibb.co/RPb4175/image.png)

**Change JDK version**
* go to file > project Structure

![alt text](https://i.ibb.co/JRcs6RK/image.png)
* in SDK change the version

**Plugins**
* install `JPA Buddy`
* Create a new package `com.ums.entity`
* Create a JPA Entity
![alt text](https://i.ibb.co/Qfz7HV6/image.png)
![alt text](https://i.ibb.co/7t0NK39/image.png)
* Click JPA Designer on top right corner
![alt text](https://i.ibb.co/qpmsnpc/image.png)
* double click Basic Type
![alt text](https://i.ibb.co/56FFqfx/image.png)
![alt text](https://i.ibb.co/RCyKVLZ/image.png)
* create all required columns like this
    * name
    * username
    * emailId
    * password
* to generate getters and settors use lombok annotation
  * @Getter
  * @Setter
  * @Data

@Data lombok anotation will automatic getters and setters internally and reduce the number of lines.
Older versions of lombok doesnot have @Data, so if @Data doesnet work then use @Getter @Setter

* create a JPA repository inside `com.ums.repository` package
![alt text](https://i.ibb.co/4Pq0mdN/image.png)
![alt text](https://i.ibb.co/pZfSG8m/image.png)
* select entity class then create
* Go to `application.properties` file
```properties
spring.application.name=ums
spring.datasource.url=jdbc:mysql://localhost:3306/ums_db
spring.datasource.username=root
spring.datasource.password=system
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```
* to run spring boot app, go to `com.ums/UmsApplication.java` run the class