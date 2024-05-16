**list all the properties by location or country name**

```java
public interface PropertyRepository extends JpaRepository<Property, Long> {

    @Query("select p from Property p join Location l on p.location = l.id join Country c on p.country=c.id where l.locationName=:locationName or c.countryName=:locationName")
    List<Property> listPropertyByLocationOrCountryName(@Param("locationName") String locationName);
}
```

```java
@GetMapping
    public ResponseEntity<List<Property>> getPropertyList(@RequestParam String locationName){
        return new ResponseEntity<List<Property>>(propertyRepository.listPropertyByLocationOrCountryName(locationName), HttpStatus.OK);
    }
```

![alt text](https://i.ibb.co/9vtWgt8/image.png)

**Review System**

![alt text](https://i.ibb.co/dgckChK/image.png)

* Create review entity and repository

```java
public interface ReviewRepository extends JpaRepository<Review, Long> {

    @Query("select r from Review r where r.property =:property and r.appUser=:user ")
    Review checkReviewExist(@Param("property") Property property,@Param("user") AppUser user);
}
```

```java
@RestController
@RequestMapping("/api/v1/reviews")
public class ReviewController {

    private ReviewRepository reviewRepository;
    private PropertyRepository propertyRepository;

    public ReviewController(ReviewRepository reviewRepository, PropertyRepository propertyRepository) {
        this.reviewRepository = reviewRepository;
        this.propertyRepository = propertyRepository;
    }

    @PostMapping
    public ResponseEntity<String> addReview(
            @AuthenticationPrincipal AppUser user,
            @RequestBody Review review,
            @RequestParam long propertyId
    ) {
        review.setAppUser(user);
        Property property = propertyRepository.findById(propertyId).get();
        review.setProperty(property);
        Review r = reviewRepository.checkReviewExist(property, user);
        if (r!= null) {
            return new ResponseEntity<>("Review already exists", HttpStatus.CONFLICT);
        }
        Review savedReview = reviewRepository.save(review);
        return new ResponseEntity<>("Review added", HttpStatus.CREATED);
    }
}
```

