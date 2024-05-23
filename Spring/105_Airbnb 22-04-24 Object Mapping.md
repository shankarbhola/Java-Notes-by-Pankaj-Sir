### Convetring List of Entity to List of Dto ###

**Method 1** (Using method)

```java
@GetMapping
    public ResponseEntity<?> getAllProperty(){
        List<Property> all = propertyRepository.findAll();
        List<PropertyDto> dtos = all.stream().map(property -> propertyToDto(property)).collect(Collectors.toList());
        return new ResponseEntity<>(dtos, HttpStatus.OK);
    }

    public PropertyDto propertyToDto(Property property){
        PropertyDto dto = new PropertyDto();
        dto.setId(property.getId());
        dto.setPropertyName(property.getPropertyName());
        dto.setGuests(property.getGuests());
        dto.setBedrooms(property.getBedrooms());
        dto.setBeds(property.getBeds());
        dto.setBathrooms(property.getBathrooms());
        dto.setNightlyPrice(property.getNightlyPrice());
        dto.setCountry(property.getCountry());
        dto.setLocation(property.getLocation());
        return dto;
    }
```

**Method 2** (Using third party library)

* for object mapping , one of the popular library is **ModelMapper**
* go to mvn repository and search for ModelMapper
* add the dependency to pom.xml file

```xml
<!-- https://mvnrepository.com/artifact/org.modelmapper/modelmapper -->
<dependency>
    <groupId>org.modelmapper</groupId>
    <artifactId>modelmapper</artifactId>
    <version>3.2.0</version>
</dependency>
```

* then add ModelMapper field with dependency injection in the class
* if you run the project then it will show error because , for third-party classes, Spring IoC won't automatically know how to instantiate these classes unless they are configured properly
* so , you can define a bean for the third-party class in a configuration class using @Bean annotation.
* can write the method in any configuration class

```java
@Configuration
public class ModelMapperConfig {

    @Bean
    public ModelMapper modelMapper() {
        return new ModelMapper();
    }
}
```
* Or you can write the method in @SpringBootApplication class because it is also a configuration class

```java
@SpringBootApplication
public class UmsApplication {

    public static void main(String[] args) {
        SpringApplication.run(UmsApplication.class, args);
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

}
```
* using modelMapper , call the map method and supply the source object and destination class
```java
modelMapper.map(property,PropertyDto.class)
```

**Converting List of items**

```java
@GetMapping
    public ResponseEntity<?> getAllProperty(){
        List<Property> all = propertyRepository.findAll();
        List<PropertyDto> dtos = all.stream().map(property -> modelMapper.map(property,PropertyDto.class)).collect(Collectors.toList());
        return new ResponseEntity<>(dtos, HttpStatus.OK);
    }
```