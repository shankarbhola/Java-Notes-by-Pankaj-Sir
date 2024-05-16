API
-
An API (Application Programming Interface) serves as a conduit for software applications to interact, defining protocols and data formats for seamless communication. It enables developers to integrate functionalities across different applications, facilitating interoperability and innovation while streamlining development processes through standardized methods of accessing and exchanging information.

![](https://i.ibb.co/MR4Ff7z/image.png)

---

![](https://i.ibb.co/fSc84kR/image.png)

---

**Certainly, here are five main points illustrating how APIs help us:**

1. **Integration**: APIs facilitate seamless connection and communication between different software systems and services, enabling them to work together efficiently.
  
2. **Efficiency**: They streamline development processes by providing pre-built functionalities, reducing the time and resources required to create new applications.

3. **Interoperability**: APIs ensure compatibility and smooth interaction between diverse software applications, allowing them to share data and functionality seamlessly.

4. **Innovation**: APIs empower developers to leverage existing capabilities and build upon them, fostering creativity and the development of new and enhanced applications.

5. **Scalability**: APIs support the growth of applications by providing a structured approach to accessing resources and services, allowing them to handle increasing amounts of data and users effectively.

**Microservices**
![](https://i.ibb.co/xzrZGmT/image.png)

Create a class inside controller layer
```java
package com.webapp.controller;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.webapp.entity.Registration;
import com.webapp.repository.RegistrationRepository;

@RestController
@RequestMapping("/api/marketing")
public class RegistrationRestController {

	@Autowired
	private RegistrationRepository registrationRepository;
	
	@GetMapping
	public List<Registration> getAllReg(){
		//localhost:8080/api/marketing
		List<Registration> registrations = registrationRepository.findAll();
		return registrations;
	}
}
```
![](https://i.ibb.co/qyXc81n/image.png)

APIs typically utilize URLs to provide endpoints for accessing data or services. They commonly return data in JSON format, comprising key-value pairs for easy parsing. While URLs and JSON are prevalent, APIs are not exclusively defined by these features, as they can use various protocols and data formats.

![](https://i.ibb.co/ZGQ93hG/image.png)
