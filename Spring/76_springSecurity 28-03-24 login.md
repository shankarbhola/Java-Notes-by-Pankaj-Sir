**Develop a login feature**
* create a `LoginDto` inside payload package

```java
package com.ums.payload;

import lombok.Data;

@Data
public class LoginDto {
    private String username;
    private String password;
}

```

* Create a login method inside AuthController
* check the username and password comes to backend or not

```java
 @PostMapping("/login")
    public  ResponseEntity<String> login(@RequestBody LoginDto loginDto){
        System.out.println(loginDto.getUsername());
        System.out.println(loginDto.getPassword());
        return new ResponseEntity<>("Login Successfull",HttpStatus.OK);
    }
```
* after checking, send value to service layer and return a boolean value
```java
@PostMapping("/login")
    public  ResponseEntity<String> login(@RequestBody LoginDto loginDto){
        boolean status = userService.verifyLogin(loginDto);
        if (status){
        return new ResponseEntity<>("Login Successfull",HttpStatus.OK);
        }
        return new ResponseEntity<>("Invalid Credentials",HttpStatus.UNAUTHORIZED);
    }
```

* then go to repository layer and create a method `findByUsername`

![alt text](https://i.ibb.co/MVjSff4/image.png)

![alt text](https://i.ibb.co/TqyrW2y/image.png)

![alt text](https://i.ibb.co/MSTZfqx/image.png)

![alt text](https://i.ibb.co/7JfQK1d/image.png)

* it will generate a method
* change class type to optional 

```java
public interface AppUserRepository extends JpaRepository<AppUser, Long> {

    Optional<AppUser> findByUsername(String username);
}
```
* create a `verifyLogin` method inside service

```java
@Override
    public boolean verifyLogin(LoginDto loginDto) {
        Optional<AppUser> opUser = userRepository.findByUsername(loginDto.getUsername());
        if (opUser.isPresent()) {
            AppUser user = opUser.get();
            return BCrypt.checkpw(loginDto.getPassword(),user.getPassword());
        }
        return false;
    }
```