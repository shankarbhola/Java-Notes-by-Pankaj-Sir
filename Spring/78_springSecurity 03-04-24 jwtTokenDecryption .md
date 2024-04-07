![alt text](https://i.ibb.co/hXVsqb0/image.png)

* `/api/v1/countries/addCountry` this url is authenticated , this url will not work until or unless the token is goes with this url and the token is validated
* when we go to this authenticated url, here should be some method that this url will goto
* login url will be go to login method , add user url will be go to add user method 
* all authenticated url has to go to a particular method where the token will be validated
* go to config and create a class named `JWTResponseFilter`
* & this class extends `OncePerRequestFilter`
* then oerride unimplimented one mrthod called `doFilterInternal`
* all authenticated url that directly comes to this method
```java
public class JWTResponseFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {

    }
}
```
* All authenticated urls can be accessed with this `request` object

* with the url header a part is called authorization 
![alt text](https://i.ibb.co/w4s6VK3/image.png)

* with the url the token is going to backend of the code and the token is hidden, with the header it is goes to the doFilterInternal method, and the token starts with `Beare `
```java
public class JWTResponseFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        String tokenHeader = request.getHeader("Authorization");
        System.out.println(tokenHeader);
    }
}
```
* go to login and generate a token
* and send the token with the url

![alt text](https://i.ibb.co/0yPXB86/image.png)

add the token with double quotes

* but this will not work, we have to tell springboot to run the doFilter method first because this method will extract the token
* first apply @Component on JWTResponseFilter class because this will handover the clas to springboot
* spring boot will create its bean, execute the bean and destroy the bean
* Go to SecurityConfig and create bean with dependency injection for JWTResponseFilter and initialize it with constructor
* then add this filter
```java
http.addFilterBefore(jwtResponseFilter, AuthorizationFilter.class);
```
```java
@Configuration
public class SecurityConfig {

    private JWTResponseFilter jwtResponseFilter;

    public SecurityConfig(JWTResponseFilter jwtResponseFilter) {
        this.jwtResponseFilter = jwtResponseFilter;
    }

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.csrf().disable().cors().disable();
        http.addFilterBefore(jwtResponseFilter, AuthorizationFilter.class);
        http.authorizeHttpRequests().
                requestMatchers("/api/v1/users/adduser","/api/v1/users/login").permitAll().
                anyRequest().authenticated();
        return http.build();
    }

}

```

* now doFilterInternal method will be run
Now we have to extract the token because token consists of Bearer

**Validate token**
we check the token issuer name, payload details by decrypting the token
* we extract the username from the token
* now this user name we will go to the database and  fatech data from databse
* when we get the record from db now we will set a session for it
*  once session is set , url is authenticated and response is given back
* once the session is set now the server know all the request is coming from which user
* Go to JWTService
* Now we require ROSI and BUVE
* R = require
* O = algorithm
* S = withissuer
* I = issuer
* BU = build
* Ve = verify

```java
public String getusername(String token) {
        DecodedJWT decodedJWT = JWT.require(algorithm).withIssuer(issuer).build().verify(token);
        return decodedJWT.getClaim("username").asString();
    }
```
* Go to JWTResponseFilter and call this method
* for calling this decryption method to get the username we have to create a constructor based dependency injection
* after that call this method
* set the request and response for filterChain method argument 
```java
@Component
public class JWTResponseFilter extends OncePerRequestFilter {

    private JWTService jwtService;

    public JWTResponseFilter(JWTService jwtService) {
        this.jwtService = jwtService;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        String tokenHeader = request.getHeader("Authorization");
        if(tokenHeader != null && tokenHeader.startsWith("Bearer ")) {
            String token = tokenHeader.substring(8,tokenHeader.length() - 1);
            String username = jwtService.getusername(token);
            System.out.println(username);
        }
        filterChain.doFilter(request, response);
    }
}
```

* while generating and verifying the token we need the claim for payload and set & get the username
* so set this to final static string
```java
@Service
public class JWTService {
    @Value("${jwt.algorithm.key}")
    private String algorithmKey;

    @Value("${jwt.issuer}")
    private String issuer;

    @Value("${jwt.expiryDuration}")
    private int expiryTime;

    private Algorithm algorithm;

    private final  static String UserName="username";
    @PostConstruct
    public void postConstruct(){
        algorithm = Algorithm.HMAC256(algorithmKey);
    }

    public String generateToken(AppUser user) {
        return JWT.create().withClaim(UserName, user.getUsername()).
                withExpiresAt(new Date(System.currentTimeMillis()+expiryTime)).
                withIssuer(issuer).
                sign(algorithm);
    }

    public String getusername(String token) {
        DecodedJWT decodedJWT = JWT.require(algorithm).withIssuer(issuer).build().verify(token);
        return decodedJWT.getClaim(UserName).asString();
    }
}

```
