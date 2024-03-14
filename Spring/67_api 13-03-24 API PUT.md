**@PostMapping**
it is used for save registration
```java
@PostMapping
	public void saveRegistration(@RequestBody Registration registration) {
		registrationRepository.save(registration);
	}
```
![](https://i.ibb.co/C8h3Hb8/image.png)

**@PutMapping**
is used for update registration
**Method-1**
Using request paramerer
```java
@PutMapping
public void updateRegistration(@RequestBody RegistrationDto dto) {
    Registration registration = new Registration();
    registration.setId(dto.getId());
    registration.setFirstName(dto.getFirstName());
    registration.setLastName(dto.getLastName());
    registration.setEmail(dto.getEmail());
    registration.setMobile(dto.getMobile());
    
    registrationRepository.save(registration);
}
```
![](https://i.ibb.co/Yc1Y95s/image.png)

**Method-2**
Using path variable
```java
//http://localhost:8080/api/marketing/1
@PutMapping("/{id}")
public void updateRegistration(@RequestBody RegistrationDto dto, @PathVariable long id) {
    Registration registration = new Registration();
    registration.setId(id);
    registration.setFirstName(dto.getFirstName());
    registration.setLastName(dto.getLastName());
    registration.setEmail(dto.getEmail());
    registration.setMobile(dto.getMobile());
    
    registrationRepository.save(registration);
}
```
![](https://i.ibb.co/c6wDrzB/image.png)

**Method-3**
Using request parameter
```java
@PutMapping
public void updateRegistration(@RequestBody RegistrationDto dto, @RequestParam long id) {
    Registration registration = new Registration();
    registration.setId(id);
    registration.setFirstName(dto.getFirstName());
    registration.setLastName(dto.getLastName());
    registration.setEmail(dto.getEmail());
    registration.setMobile(dto.getMobile());
    
    registrationRepository.save(registration);
}
```
![](https://i.ibb.co/1vSKSMY/image.png)