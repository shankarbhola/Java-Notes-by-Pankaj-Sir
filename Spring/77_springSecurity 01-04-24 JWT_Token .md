JWT Token
-

JWT (JSON Web Token) tokens are used for securely transmitting information between parties. They authenticate users by encoding claims like user identity and permissions into a compact format. These tokens enable stateless communication, allowing servers to validate and trust the information without storing session data.

![alt text](https://i.ibb.co/z4rsbV2/image.png)

* client send the username + password to backend
*  then backend validate the username and password and return back something called token that is JWT token to client
*  client can be angular, can be postman, anything....

![alt text](https://i.ibb.co/3zdMQzh/image.png)

**Encryption Technique**
1. Algorithm - While generating a tocken what algoruthm to use
2. Secret Key - What password to give
3. Issuer name - What issuer name to give
4. Expiry - Set a expiry time on your tocken

A JWT token consists of three main parts:
1. **Header:** Contains metadata such as the type of token and the cryptographic algorithm used for signing.

2. **Payload:** Contains claims or statements about the entity (e.g., user) and additional data. It's often divided into reserved and custom claims.

3. **Signature:** Created by encoding the header, payload, and a secret key using the specified algorithm. It ensures the integrity and authenticity of the token.

Go to JWT official website [(https://jwt.io/)](https://jwt.io/)

Structure of JWT Token

![alt text](https://i.ibb.co/6bsdd43/image.png)

Red colour part is header
purple colour part is payload
blue colour is signature

**Create JWT token**
* go to service layer & create a class named `JWTService`
* go to application.prpperties file and add a key value for secret key like this
```properties
jwt.algorithm.key=6uW1lf-0CPAul-B4ew37-yxOOip-T2Lwzu
```
* set a random password for token encryption

* go to JWTService class and create a variable
```java

@Service
public class JWTService {
    @Value("${jwt.algorithm.key}")
    private String algorithmKey;
}
```

* when run the application this class will run automatically and whatever the value present in properties file it will initialize the variable
* like this create an issuer name
```properties
jwt.issuer=shankar
```
```java
@Value("${jwt.issuer}")
    private String issuer;
```

* Expiry time for token will be given in milisecond
```properties
jwt.expiryDuration=86400000
```
```java
@Value("$jwt.expiryDuration}")
    private int expiryTime;
```

* for algorithm go to [text](https://jwt.io/libraries)
* filter it by selecting java
* Every JWT token library has certain supported algorithm

![alt text](https://i.ibb.co/pPpkXqk/image.png)

* according to requirement pick one of the library
* com.auth0 / java-jwt library has expiry check so we can use this library
* go to google & search for `com.auth0 / java-jwt`
* go to mvm repository webside and pick ony version 
* in order to get the algorithm put the dependency on pom.xml file
* create a algorithm variable for create algorithm
```java
@Service
public class JWTService {
    @Value("${jwt.algorithm.key}")
    private String algorithmKey;

    @Value("${jwt.issuer}")
    private String issuer;

    @Value("$jwt.expiryDuration}")
    private int expiryTime;

    private Algorithm algorithm;

}
```
* Create a postConstruct method and apply @PostConstruct annotation on this method
* this method will run automatically after start the project

![alt text](https://i.ibb.co/TkN9b3N/image.png)

```java
@PostConstruct
    private void postConstruct(){
        algorithm = Algorithm.HMAC256(securityKey);
    }
```

**Generate a token**
```java
public String generateToken(AppUser user) {
        return JWT.create().
                withClaim("username", user.getUsername()).
                withExpiresAt(new Date(System.currentTimeMillis()+expiryTime)).
                withIssuer(issuer).
                sign(algorithm);
    }
```
* Remember the word `Computer engineer is unemployed`
1. C = withClaim("name", user.getName())
    it is used to set payload details
2. E = withExpiresAt(new Date(System.currentTimeMillis()
    it is used to set the token expiry duration
3. I = withIssuer(issuer)
    it is used to set the issuer name
4. S = sign(algorithm)
    it is used to sign the algorithm and create the token. It returns a string value


**Where to use**
* in service layer, after verify thr username and password, we can call this method and return the string token to controller layer
* before that we have to creat constructor based dependency injection for JWTService in service layer

```java
//service
@Override
    public String verifyLogin(LoginDto loginDto) {
        Optional<AppUser> opUser = userRepository.findByUsernameOrEmailId(loginDto.getUsername(), loginDto.getEmailId());
        if (opUser.isPresent()) {
            AppUser user = opUser.get();
            if (BCrypt.checkpw(loginDto.getPassword(),user.getPassword())){
                return jwtService.generateToken(user);
            }
        }
        return null;
    }
```
* it will goes back to controller and return the token

```java
//authcontroller
@PostMapping("/login")
    public  ResponseEntity<String> login(@RequestBody LoginDto loginDto){
        String token = userService.verifyLogin(loginDto);
        if (token!=null){
        return new ResponseEntity<>(token,HttpStatus.OK);
        }
        return new ResponseEntity<>("Invalid Credentials",HttpStatus.UNAUTHORIZED);
    }
```

**Set authenticated urls**
create a add country url
* go to controlller create a `countryController` class and apply @Component on it

```java
@RestController
@RequestMapping("/api/v1/countries")
public class CountryController {

    @PostMapping("/addCountry")
    public String addCountry(){
        return "done";
    }
}
```
* then go to securityFilterChain method in SecurityConfig class
```java
@Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.csrf().disable().cors().disable();
        http.authorizeHttpRequests().
                requestMatchers("/api/v1/users/adduser","/api/v1/users/login").permitAll().
                anyRequest().authenticated();
        return http.build();
    }
```
* now `/api/v1/countries/addCountry` this url is authenticated url
