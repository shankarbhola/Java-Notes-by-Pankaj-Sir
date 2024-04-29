**Uploading Images**

![alt text](https://i.ibb.co/ctvcndf/image.png)

* create an images entity

```java
package com.ums.Entity;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
@Entity
@Table(name = "images")
public class Images {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id", nullable = false)
    private Long id;

    @Column(name = "image_url", nullable = false, length = 1000)
    private String imageUrl;

    @ManyToOne
    @JoinColumn(name = "property_id")
    private Property property;

}
```

* Create a repository for image entity
* Create a controller layer

```java
package com.ums.controller;

import com.ums.Entity.Images;
import com.ums.Entity.Property;
import com.ums.repository.ImagesRepository;
import com.ums.repository.PropertyRepository;
import com.ums.service.BucketService;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.MultipartFile;

@RestController
@RequestMapping("/api/v1/images")
public class ImageController {

    private ImagesRepository imagesRepository;
    private PropertyRepository propertyRepository;
    private BucketService bucketService;

    public ImageController(ImagesRepository imagesRepository, PropertyRepository propertyRepository, BucketService bucketService) {
        this.imagesRepository = imagesRepository;
        this.propertyRepository = propertyRepository;
        this.bucketService = bucketService;
    }

    @PostMapping("/addImage")
    public ResponseEntity<Images> addImages(
            @RequestParam long propertyId,
            @RequestParam String bucketName,
            MultipartFile file
    ) {
        String imageUrl = bucketService.uploadFile(file, bucketName);
        Property property = propertyRepository.findById(propertyId).get();
        Images image = new Images();
        image.setImageUrl(imageUrl);
        image.setProperty(property);
        return new ResponseEntity<>(imagesRepository.save(image), HttpStatus.CREATED);
    }
}

```

![alt text](https://i.ibb.co/WD1CtH8/image.png)

* the image url for property is saved on database

![alt text](https://i.ibb.co/1YN2VK0/image.png)



**Find all images of a property**

```java
public interface ImagesRepository extends JpaRepository<Images, Long> {
    List<Images> findByProperty_Id(Long id);
}
```

```java
@GetMapping("/propertyImages")
    public ResponseEntity<?> fetchPropertyImages(@RequestParam long propertyId) {
        List<Images> images = imagesRepository.findByProperty_Id(propertyId);
        if (images.isEmpty()) {
            return new ResponseEntity<>("No images found", HttpStatus.NOT_FOUND);
        }
        return new ResponseEntity<>(images, HttpStatus.OK);
    }
```

![alt text](https://i.ibb.co/mRW5R6P/image.png)

