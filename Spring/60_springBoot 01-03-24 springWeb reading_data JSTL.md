### Third way of Reading data ###
create a  Data Transfer Object (DTO) layer
* create a package named ```com.webapp.dto``` inside ```src/main/java```
* Create a simple java class named ```RegistrationDto.java```

```java
//RegistrationDto.java
package com.webapp.dto;

public class RegistrationDto {
	private String firstName;
	private String lastName;
	private String email;
	private String mobile;
	public String getFirstName() {
		return firstName;
	}
	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public void setLastName(String lastName) {
		this.lastName = lastName;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getMobile() {
		return mobile;
	}
	public void setMobile(String mobile) {
		this.mobile = mobile;
	}
	
}
```

in controller use dto object
```java
//RegistrationController.java
package com.webapp.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;

import com.webapp.dto.RegistrationDto;
import com.webapp.entity.Registration;
import com.webapp.service.RegistrationService;

@Controller
public class RegistrationController {
	
	@RequestMapping("/view-reg-page")
	public String viewRegistrationPage() {
		return "registration";
	}
	
	@Autowired
	private RegistrationService res;
	
	@RequestMapping("/saveReg")
	public String addRegistration(RegistrationDto dto) {
		Registration registration = new Registration();
		registration.setFirstName(dto.getFirstName());
		registration.setLastName(dto.getLastName());
		registration.setEmail(dto.getEmail());
		registration.setMobile(dto.getMobile());
		res.addRegistration(registration);
		return "registration";
	}
}
```
### JSTL tag(JSP Standard tag Library) ###
![JSTL](https://i.ibb.co/X7NR8sP/image.png)
![](https://i.ibb.co/pwsR2zG/image.png)

* JSTL is old technology
* we cannot use in java 17
* we have to change older java version 8
* also change spring version to 2.7.17
* go to pom.xml file and change this
* when we run the project it will show error
* when we change java 17 to 8 we have to ```jakarta``` to ```javax```
* go to entity class and replace
* go to [mvnrepository](https://mvnrepository.com/)
* search **jstl jar**
* v1.2 copy dependency and paste it in pom.xml