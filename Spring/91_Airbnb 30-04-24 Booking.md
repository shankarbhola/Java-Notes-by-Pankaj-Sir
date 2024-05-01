* create repository for booking entity
* create controller

```java
package com.ums.controller;

import com.ums.Entity.AppUser;
import com.ums.Entity.Bookings;
import com.ums.Entity.Property;
import com.ums.repository.BookingsRepository;
import com.ums.repository.PropertyRepository;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/v1/booking")
public class BookingController {

    private BookingsRepository bookingsRepository;
    private PropertyRepository propertyRepository;

    public BookingController(BookingsRepository bookingsRepository, PropertyRepository propertyRepository) {
        this.bookingsRepository = bookingsRepository;
        this.propertyRepository = propertyRepository;
    }

    @PostMapping("/addBooking")
    public ResponseEntity<?> createBooking(
            @RequestBody Bookings bookings,
            @RequestParam long propertyId,
            @AuthenticationPrincipal AppUser user
            ){
        Property property = propertyRepository.findById(propertyId).get();
        bookings.setAppUser(user);
        bookings.setProperty(property);
        bookings.setTotalPrice(property.getNightlyPrice() * bookings.getTotalNights());
        Bookings savedBooking = bookingsRepository.save(bookings);
        return new ResponseEntity<>(savedBooking, HttpStatus.CREATED);
    }
}

```

![alt text](https://i.ibb.co/gyR2MqS/image.png)