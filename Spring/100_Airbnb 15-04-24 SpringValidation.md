## Spring Validation ##

**Step 1**
* go to spring initializer and find the dependency and add it on the project in pom.xml file

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

**Step 2**
* add validations on the dto class

```java
package com.ums.payload;

import jakarta.validation.constraints.Email;
import jakarta.validation.constraints.NotNull;
import jakarta.validation.constraints.Pattern;
import jakarta.validation.constraints.Size;
import lombok.Data;

@Data
public class UserDto {
    private Long id;

    @NotNull(message = "Name cannot be null")
    @Size(min = 2, max = 50, message = "Name must be between 2 and 50 characters")
    private String name;

    @NotNull(message = "Username cannot be null")
    @Size(min = 5, max = 20, message = "Username must be between 5 and 20 characters")
    private String username;

    @NotNull(message = "Email cannot be null")
    @Email(message = "Email should be valid")
    private String emailId;

    @NotNull(message = "Password cannot be null")
    @Size(min = 8, message = "Password must be at least 8 characters")
    @Pattern(regexp = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z]).*$", message = "Password must contain at least one digit, one lowercase letter, and one uppercase letter")
    private String password;

    private String userRole;
}
```

**Step 3**
* return the error as response to client

**Step 4**
* add **BindingResult** as method parameter and if error occurs then return the it

**Step 4**
add **@Valid** annotation before dto method parameter

```java
@PostMapping("/{adduser}")
    public ResponseEntity<?> adduser(@Valid @RequestBody UserDto userdto, BindingResult bindingResult) {
        if (bindingResult.hasErrors()){
            return new ResponseEntity<>(bindingResult.getFieldError().getDefaultMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
        }
        UserDto dto = userService.addUser(userdto);
        return new ResponseEntity<>(dto, HttpStatus.CREATED);
    }
```
