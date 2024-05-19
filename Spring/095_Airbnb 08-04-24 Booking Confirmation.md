* from the booking controller , after saving data on database , call the method inside the pdfservice and supply the property and booking object
* It will return path of the file
* but now we upload the file and send the confirmation pdf link using sms
* for uploading file we need a multipartfile
* we have to convert the path of the file to multipartfile 
* in booking controller create a method to convert file path to multipart file

```java
public static MultipartFile convert(String filePath) throws IOException {
        File file = new File(filePath);
        FileInputStream inputStream = new FileInputStream(file);
        MockMultipartFile multipartFile = new MockMultipartFile(file.getName(), file.getName(), MediaType.MULTIPART_FORM_DATA_VALUE, inputStream);
        return multipartFile;
    }
```

**Note**
<br>
If you getting erron on `MockMultipartFile` then add the below dependency

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
</dependency>
```

* if we upload the file into s3 bucket it will return a long url
* if we send this url in sms , the cost of the sms will double
* so that we have to short the url
* for shorting url , we will use [bit.ly](https://bit.ly)
* signup, then go to settings, API

![alt text](https://i.ibb.co/54z3RqR/image.png)

* Enter the password then click on generate token
* add the token in properties file

![alt text](https://i.ibb.co/vDkL9bt/image.png)


```properties
bitly_token=****************************************
```

* create a service class for bitly

```java
package com.ums.service;

import com.opsmatters.bitly.Bitly;
import com.opsmatters.bitly.api.model.v4.CreateBitlinkResponse;
import jakarta.annotation.PostConstruct;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

@Service
public class BitlyService {

    @Value("${bitly_token}")
    String BITLY_TOKEN;

    private Bitly client;

    @PostConstruct
    public void setup() {
        client = new Bitly(BITLY_TOKEN);
    }

    public String shortLink(String longURL) {

        try {
            CreateBitlinkResponse response = client.bitlinks().shorten(longURL).get();
            String link = response.getLink();
            return link;
        }
        catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

* inside the addBooking method call the pdf generation method, it will return the file path
* convert it into Multipart file
* upload it in s3 bucket, it will return the url
* after upload file into s3 bucket, delete the local file
* short the url using bitly
* send the sms with the pdf shorted link


```java
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
        String filePath = pdfService.generateBookingDetailsPDF(bookings, property);
        try {
            MultipartFile file = convert(filePath);
            String url = bucketService.uploadFile(file);
            File tempFile = new File(filePath);
            tempFile.delete();
            System.out.println(url);
            String shortedLink = bitlyService.shortLink(url);
            System.out.println(shortedLink);
            smsService.sendSms("+918114944951","Your Booking is Confirmed. Click here "+shortedLink);
            return new ResponseEntity<>(savedBooking, HttpStatus.CREATED);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;

    }
```