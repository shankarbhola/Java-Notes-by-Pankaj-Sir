**Add User Role**
* first create a new column in the table
* go to entity and create a new column for useRole
* update the user role in dto and service

![alt text](https://i.ibb.co/g3xVSLv/image.png)

![alt text](https://i.ibb.co/qCpsBzC/image.png)

* now for authorization url we've supply the role in to `UsernamePasswordAuthenticationToken`

![alt text](https://i.ibb.co/9T95LjG/image.png)


<strike>

```java
UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(user,"null",user.getUserRole());
```
</strike>

* if we set the role like this it will show error because it requires the collection parameter

```java
UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(user,"null", Collections.singleton(new SimpleGrantedAuthority(user.getUserRole())));
```

* `new SimpleGrantedAuthority(user.getUserRole())` it represents a granted authority for an authentication object. This authority typically corresponds to a role or permission that a user possesses. 

* `Collections.singleton()` This method is particularly useful when you need to pass a single element as an argument to a method that expects a collection

Now set the authorization url for admin and user

```java
http.authorizeHttpRequests()
                .requestMatchers("/api/v1/auth/adduser","/api/v1/auth/login").permitAll()
                .requestMatchers("/api/v1/countries/addCountry").hasRole("ADMIN")
                .requestMatchers("/api/v1/auth/profile").hasAnyRole("ADMIN","USER")
                .anyRequest().authenticated();
```