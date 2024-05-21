
![alt text](https://i.ibb.co/8x3hTgc/image.png)

* Create entity class for favourite

```java
@Getter
@Setter
@Entity
@Table(name = "favourite")
public class Favourite {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", nullable = false)
    private Long id;

    @Column(name = "is_favourite")
    private Boolean isFavourite;

    @ManyToOne
    @JoinColumn(name = "app_user_id")
    private AppUser appUser;

    @ManyToOne
    @JoinColumn(name = "property_id")
    private Property property;

}
```

```java
public interface FavouriteRepository extends JpaRepository<Favourite, Long> {

    @Query("select f from Favourite f where f.appUser =:user and f.property=:property")
    Favourite checkReviewExists(@Param("user") AppUser user,@Param("property") Property property);

}
```

```java
package com.ums.controller;

import com.ums.Entity.AppUser;
import com.ums.Entity.Favourite;
import com.ums.Entity.Property;
import com.ums.repository.FavouriteRepository;
import com.ums.repository.PropertyRepository;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/v1/favorite")
public class FavouriteController {

    private FavouriteRepository favouriteRepository;
    private PropertyRepository propertyRepository;

    public FavouriteController(FavouriteRepository favouriteRepository, PropertyRepository propertyRepository) {
        this.favouriteRepository = favouriteRepository;
        this.propertyRepository = propertyRepository;
    }

    @PostMapping("/addFav")
    public ResponseEntity<?> addFavourite(
            @AuthenticationPrincipal AppUser user,
            @RequestParam long PropertyId
    ){
        Property property = propertyRepository.findById(PropertyId).get();

        Favourite favourite = new Favourite();
        favourite.setAppUser(user);
        favourite.setProperty(property);
        Favourite byAppUserIdAndPropertyId = favouriteRepository.checkReviewExists(user, property);
        if (byAppUserIdAndPropertyId == null) {
            favourite.setIsFavourite(true);
            Favourite savedFavourite = favouriteRepository.save(favourite);
            return new ResponseEntity<>(savedFavourite, HttpStatus.OK);
        }
        if (byAppUserIdAndPropertyId != null) {
            favouriteRepository.deleteById(byAppUserIdAndPropertyId.getId());
            return new ResponseEntity<>("Removed From Favourite", HttpStatus.OK);
        }

        return new ResponseEntity<>("Something Wrong", HttpStatus.BAD_REQUEST);
    }

}

```

**Users Favourite List**

```java
@Query("select f from Favourite f where f.appUser =:user")
    List<Favourite> findAllByAppUser(@Param("user") AppUser user);
```
```java
@GetMapping("/userFavList")
    public ResponseEntity<?> getAllFavouritesOfUser(@AuthenticationPrincipal AppUser user){
        return new ResponseEntity<>(favouriteRepository.findAllByAppUser(user), HttpStatus.OK);
    }
```

