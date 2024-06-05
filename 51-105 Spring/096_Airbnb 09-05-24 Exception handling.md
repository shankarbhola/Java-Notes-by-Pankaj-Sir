**Exception**

* create a package named `exceptions`
* inside this package create a class

```java
package com.ums.exceptions;

public class ResourceNotFound extends RuntimeException{
    public ResourceNotFound(String message){
        super(message);
    }
}

```

* inside the property controller create a method for ge the property details using property id

```java
@GetMapping("/{propertyId}")
    public ResponseEntity<?> getPropertyById(@PathVariable long propertyId){
        Property property = propertyRepository.findById(propertyId).orElseThrow(
                ()-> new ResourceNotFound("Property not found with id "+propertyId)
        );
        return new ResponseEntity<>(property,HttpStatus.OK);
    }
```

![alt text](https://i.ibb.co/W20CnXr/image.png)

* whrn the resource not found, it will throw the custom exception class
* we are throwing the exception but now we will handle the exception
* now we will develop a control advice class to handle this exception
* @ControllerAdvice is a specialized form of the spring's stereotype annotation which allows handling exceptions across the whole application in one global handling component

```java
package com.ums.exceptions;

import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFound.class)
    public ResponseEntity<?> resourceNotFound(ResourceNotFound exception){
        return new ResponseEntity<>(exception.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }

}

```

![alt text](https://i.ibb.co/wN6CSJH/image.png)

* Now we handle the exception more clear 
* we will return the date and time when the exception occurs and where the exception occurs
* for that create a payload for exception inside the payload package

```java
package com.ums.payload;

import lombok.Getter;

import java.util.Date;

@Getter
public class ErrorDetails {
    private String message;
    private Date date;
    private String description;

    public ErrorDetails(String message, Date date, String description){
        this.message=message;
        this.date=date;
        this.description = description;
    }
}

```

* here webRequest will help to get the url , where the exception occurs

```java
package com.ums.exceptions;

import com.ums.payload.ErrorDetails;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.context.request.WebRequest;

import java.util.Date;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFound.class)
    public ResponseEntity<?> resourceNotFound(ResourceNotFound exception, WebRequest webRequest){
        ErrorDetails errorDetails = new ErrorDetails(exception.getMessage(),new Date(),webRequest.getDescription(false));
        return new ResponseEntity<>(errorDetails, HttpStatus.INTERNAL_SERVER_ERROR);
    }

}

```

* the above code is for only resource not found exception
* if we write exceptiion for null pointer exception it will work for only null pointer exception
* if we write exceptiion for arithmatic exception it will work for only arithmatic exception
* if we use Exception class, it will handle all types of exception

```java
package com.ums.exceptions;

import com.ums.payload.ErrorDetails;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.context.request.WebRequest;

import java.util.Date;

@ControllerAdvice
public class ExceptionHandlerClass {

    @ExceptionHandler(ResourceNotFound.class)
    public ResponseEntity<?> resourceNotFound(ResourceNotFound exception, WebRequest webRequest){
        ErrorDetails errorDetails = new ErrorDetails(exception.getMessage(),new Date(),webRequest.getDescription(false));
        return new ResponseEntity<>(errorDetails, HttpStatus.INTERNAL_SERVER_ERROR);
    }

    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<?> GlobalExceptionHandler(Exception exception, WebRequest webRequest){
        ErrorDetails errorDetails = new ErrorDetails(exception.getMessage(),new Date(),webRequest.getDescription(false));
        return new ResponseEntity<>(errorDetails, HttpStatus.INTERNAL_SERVER_ERROR);
    }

}

```

* if exception is resource not found, then resourceNotFound method will run 
* if any other exception occurs, GlobalExceptionHandler method will run

