* Download [Postman](https://www.postman.com/downloads/)
* Sign in with google
* Create a workspace
* Create a new blank collection
* Add a request

* run the project and test the url in postman
```java
@GetMapping
	public List<Registration> getAllReg(){
		//localhost:8080/api/marketing
		List<Registration> registrations = registrationRepository.findAll();
		return registrations;
	}
```
GET ```http://localhost:8080/api/marketing```
* it will show all the records in json format 

To delete use @DeleteMapping
```java
@DeleteMapping
	public void delete(@RequestParam long id) {
		registrationRepository.deleteById(id);
	}
```
DELETE ```http://localhost:8080/api/marketing?id=1```
