**Create a user and give certain access to this user**

* go to search box and search `IAM`

![alt text](https://i.ibb.co/XtDzt21/image.png)

* select `IAM`
* select `users`

![alt text](https://i.ibb.co/k967rhd/image.png)

* click on create user

![alt text](https://i.ibb.co/ZB9kWrV/image.png)

* give the name of the user then click on next

![alt text](https://i.ibb.co/6tDr3Tm/image.png)

* create a group
* here a group contains set of policy 
* if a user is on that group , user can access only on that services which group contains
* for now we will add admnistrator access to this group

![alt text](https://i.ibb.co/9rWQjm9/image.png)

* now select the group and click on next

![alt text](https://i.ibb.co/FW8dZMm/image.png)

* now click on create user

![alt text](https://i.ibb.co/b1x0BYJ/image.png)

* click on user1

![alt text](https://i.ibb.co/QcXrNpB/image.png)

* go to security credentials

![alt text](https://i.ibb.co/swh5grf/image.png)

* click on `enable console access`

![alt text](https://i.ibb.co/wCnkhWw/image.png)

* select custom password & set a password for the user

![alt text](https://i.ibb.co/cJMBQyZ/image.png)

* we will get a login link 
* in order to login programmatically to s3 we have to create a access key

![alt text](https://i.ibb.co/djCdpq2/image.png)

* click on create access key

![alt text](https://i.ibb.co/72ZLCVV/image.png)

* click on next
* now download the .csv file

![alt text](https://i.ibb.co/zrC5M1V/image.png)

* now login through the user link

![alt text](https://i.ibb.co/1KSd5W3/image.png)

* go to s3

![alt text](https://i.ibb.co/tYrL04J/image.png)

* now on user1 account , we can access s3 bucket

![alt text](https://i.ibb.co/558kJh4/image.png)

* if this is root account , we can access this
* because of administrator account we cannot access this

### S3 Integration with spring boot project ###

* add the AWS s3 dependency

```xml
<dependency>
		<groupId>com.amazonaws</groupId>
		<artifactId>aws-java-sdk-s3</artifactId>
		<version>1.12.310</version>
</dependency>
```

* add this to application.properties file

```properties
accessKey=************************
secretKey=*************************
region=eu-north-1
cloud.aws.region.static=eu-north-1
cloud.aws.region.auto=false
cloud.aws.stack.audo=false
spring.main.allow-bean-definition-overriding=true
logging.level.com.amazonaws.util.EC2MetadataUtils=error
logging.level.com.amazonaws.internal.InstanceMetadataServiceResourceFetcher=error
```

* change 1st four line according to aws s3 settings

* Crete a config file for aws

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import com.amazonaws.auth.AWSCredentials;
import com.amazonaws.auth.AWSStaticCredentialsProvider;
import com.amazonaws.auth.BasicAWSCredentials;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;

@Configuration
public class AWSS3Config {

    @Value("${accessKey}")
    private String accessKey;

    @Value("${secretKey}")
    private String secretKey;

    @Value("${region}")
    private String region;

    public AWSCredentials credentials() {
        AWSCredentials credentials = new BasicAWSCredentials(accessKey, secretKey);
        return credentials;
    }

    @Bean
    public AmazonS3 amazonS3() {

        AmazonS3 s3client = AmazonS3ClientBuilder.standard()
                .withCredentials(new AWSStaticCredentialsProvider(credentials())).withRegion(region).build();
        return s3client;
    }
}
```

* create service layer

```java
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.model.AmazonS3Exception;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.web.multipart.MultipartFile;

import java.io.File;

@Service
public class BucketService {

    @Autowired
    private AmazonS3 amazonS3;

    public String uploadFile(MultipartFile file, String bucketName) {
        if (file.isEmpty()) {
            throw new IllegalStateException("Cannot upload empty file");
        }
        try {
            File convFile = new File(System.getProperty("java.io.tmpdir") + "/" + file.getOriginalFilename());
            file.transferTo(convFile);
            try {
                amazonS3.putObject(bucketName, convFile.getName(), convFile);
                return amazonS3.getUrl(bucketName, file.getOriginalFilename()).toString();
            } catch (AmazonS3Exception s3Exception) {
                return "Unable to upload file :" + s3Exception.getMessage();
            }



        } catch (Exception e) {
            throw new IllegalStateException("Failed to upload file", e);
        }

    }

//    public String deleteBucket(String bucketName) {
//        amazonS3.deleteBucket(bucketName);
//        return "File is deleted";
//    }

}
```

* create a controller layer

```java
import com.s3example1.service.BucketService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;

@RestController
@RequestMapping("s3bucket")
@CrossOrigin("*")
public class BucketController {

    @Autowired
    BucketService service;

    @PostMapping(path = "/upload/file/{bucketName}", consumes = MediaType.MULTIPART_FORM_DATA_VALUE, produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<String> uploadFile(@RequestParam MultipartFile file,
                                             @PathVariable String bucketName) {
        return new ResponseEntity<>(service.uploadFile(file,bucketName), HttpStatus.OK);
    }
}

//@DeleteMapping(path="/delete/file/{bucketName}/{fileName}")
//public ResponseEntity<String> deleteFile(@PathVariable String bucketName,@PathVariable String fileName)
//{
//    return new ResponseEntity<>(service.deleteFile(bucketName,fileName),HttpStatus.OK);
//}


```

**@CrossOrigin("*")**
* `@CrossOrigin("*")` in Spring Boot allows requests from any origin, enabling Cross-Origin Resource Sharing (CORS) for a specific controller method or the entire controller.
* Using `@CrossOrigin("*")` in Spring Boot allows requests from any origin, including those made by applications running on different servers such as Angular applications. This is particularly useful when you want to build a web service that needs to be consumed by client applications running on different domains.

Now Start the application

![alt text](https://i.ibb.co/VmP9JnK/image.png)

