### Second way of Reading data ###
**@RequestParam**
It binds data with method arguments in controller layer
```java
//RegistrationCOntroller.java
package com.webapp.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;

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
	
//	@RequestMapping("/saveReg")
//	public String addRegistration(@ModelAttribute Registration registration) {
//		res.addRegistration(registration);
//		return "registration";
//	}
	
	@RequestMapping("/saveReg")
	public String addRegistration(
			@RequestParam("xyz") String firstName,
			@RequestParam("lastName") String lastName,
			@RequestParam("email") String email,
			@RequestParam("mobile") String mobile
			) {
		Registration registration = new Registration();
		registration.setFirstName(firstName);
		registration.setLastName(lastName);
		registration.setEmail(email);
		registration.setMobile(mobile);
		res.addRegistration(registration);
		return "registration";
	}
}
```

**Display as record saved**
* add model interface in that method 

```java
@RequestMapping("/saveReg")
	public String addRegistration(Model model) {
		model.addAttribute("msg","Record Saved!!");
		return "registration";
	}
```

```java
//RegistrationController.java
package com.webapp.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;

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
	
//	@RequestMapping("/saveReg")
//	public String addRegistration(@ModelAttribute Registration registration) {
//		res.addRegistration(registration);
//		return "registration";
//	}
	
	@RequestMapping("/saveReg")
	public String addRegistration(
			@RequestParam("xyz") String firstName,
			@RequestParam("lastName") String lastName,
			@RequestParam("email") String email,
			@RequestParam("mobile") String mobile,
			Model model
			) {
		Registration registration = new Registration();
		registration.setFirstName(firstName);
		registration.setLastName(lastName);
		registration.setEmail(email);
		registration.setMobile(mobile);
		res.addRegistration(registration);
		model.addAttribute("info","Some Data");
		model.addAttribute("msg","Record Saved!!");
		return "registration";
	}
}

```
**add Devtools**
* right click on project
* go to spring
* add devtool
* when we save the changes, we need not to stop and again run the project,  it will re run automatically