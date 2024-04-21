![alt text](https://i.ibb.co/9m0YCdf/image.png)

* create entity class, repository and controller
* run the application and supply the JSON value

**list all the properties by location name**

```sql
select * from property p join location l on p.location_id=l.id where l.location_name="Ooty"
```

```java
public interface PropertyRepository extends JpaRepository<Property, Long> {

    @Query("select p from Property p join Location l on p.location = l.id where l.locationName=:locationName")
    List<Property> listPropertyByLocationOrCountryName(@Param("locationName") String locationName);
}
```

```java
@GetMapping
    public ResponseEntity<List<Property>> getPropertyList(@RequestParam String locationName){
        return new ResponseEntity<List<Property>>(propertyRepository.listPropertyByLocationOrCountryName(locationName), HttpStatus.OK);
    }
```



