**Set session for current user logged in**

* first we need complete user details 
* by username find the record

```java
//JWTResponseFilter
Optional<AppUser> opUser = appUserRepository.findByUsername(userName);
if (opUser.isPresent()) {
    AppUser appUser = opUser.get();
    //To track current user logged in
    UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(appUser,null,new ArrayList<>());
    authentication.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
    SecurityContextHolder.getContext().setAuthentication(authentication);
}
```
>UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(appUser,null,new ArrayList<>());

* here we set the principal for the current user.
* this principle holds the user details with session id
* **appUser:** This is typically the username or user object that represents the authenticated user. It is passed as the first parameter of the UsernamePasswordAuthenticationToken constructor.
* **null:** The second parameter represents the password. In this case, it's set to null because the password is not provided at this stage. It may be set later depending on your authentication mechanism.
* **new ArrayList<>():** The third parameter represents the authorities or roles granted to the user. In this case, an empty list is provided, indicating that the user has no authorities yet.

>authentication.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));

* to remember this code , remember "adani sets new world record"
* in the line, what request will come, for that request it  generate the session id because the second time the user sen the request that point of time it can track the user based on session id and give the relevent respont to that user.

>SecurityContextHolder.getContext().setAuthentication(authentication);

* remeber like this "Security guard service"
* it will save the session id in spring boot server side 
* when second time the request is come , it will check the session id in the server side 
```java
@Component
public class JWTResponseFilter extends OncePerRequestFilter {

    private JWTService jwtService;
    private AppUserRepository appUserRepository;
    public JWTResponseFilter(JWTService jwtService, AppUserRepository appUserRepository) {
        this.jwtService = jwtService;
        this.appUserRepository = appUserRepository;
    }

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        String tokenHeader = request.getHeader("Authorization");
        if (tokenHeader != null && tokenHeader.startsWith("Bearer ")) {
            String token = tokenHeader.substring(8, tokenHeader.length() - 1);
            String userName = jwtService.getUserName(token);
            Optional<AppUser> opUser = appUserRepository.findByUsername(userName);
            if (opUser.isPresent()) {
                AppUser appUser = opUser.get();
                //to track current user logged in
                UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(appUser,null,new ArrayList<>());
                authentication.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                SecurityContextHolder.getContext().setAuthentication(authentication);
            }
        }
        filterChain.doFilter(request, response);

    }
}

```
---
**current user profile loged in**
* for current user it will show only the current user profile   
* go to AuthController and create a getCurrentProfile method

```java
@GetMapping("/profile")
    public AppUser getCurrentProfile(@AuthenticationPrincipal AppUser user){
        return user;
    }
```
* here @AuthenticationPrincipal, based on the current user logged in , it will automatically for that userm it will fatch the user details and it put that into AppUser.
* so whichever user is logged in it will pick that details from principal because in usernamepasswordauthentication we setting up the principle where princeple holds the user object details and the session id
* 1st login and generate the token and session id 
* supply the token with the peofile url

![alt text](https://i.ibb.co/4TCH89T/image.png)

* here, according to the token and session id it will give us the current user information

**Response should comes as JSON object**
* JWT response means the token shoud return in JSON object format
* create a JSONResponse class in payload

```java
@Data
public class JWTResponse {
    private String type = "Bearer";
    private String token;
}

```

* after login it should return the JSON response
```java
@PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody LoginDto loginDto){
        String token = userService.login(loginDto);
        if(token!=null){
            JWTResponse response = new JWTResponse();
            response.setToken(token);
            return new ResponseEntity<>(response, HttpStatus.OK);
        }
        return new ResponseEntity<String>("Invalid Credentials", HttpStatus.UNAUTHORIZED);
    }
```

![alt text](https://i.ibb.co/h1GCzx5/image.png)