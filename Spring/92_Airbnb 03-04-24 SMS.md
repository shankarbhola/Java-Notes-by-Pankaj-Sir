**SMS**

* There is numbers of company provides sms features
* we can integrate that in our project
* There are many company, but there is one popular company ccalled twilio 
* twilio provides multiple features like, live video streaming, calls, emails, sms etc.

**Integrate Twilio to spring boot**
* go to [twilio.com](https://www.twilio.com/)
* Create a free twilio account 

![alt text](https://i.ibb.co/Gv5Pnzp/image.png)

* verify with email otp
* Enter phone number and verify otp with mobile number

![alt text](https://i.ibb.co/ZB49vJk/image.png)

![alt text](https://i.ibb.co/L0r4xDW/image.png)

![alt text](https://i.ibb.co/F7RrFqz/image.png)

![alt text](https://i.ibb.co/KXSJZsr/image.png)

![alt text](https://i.ibb.co/WFyS2rc/image.png)

* add dependency to pom.xml file
```XML
<dependency>
    <groupId>com.twilio.sdk</groupId>
    <artifactId>twilio</artifactId>
    <version>8.21.0</version> <!-- Use the latest version -->
</dependency>
```

* set the SID and Token in properties file

```properties
twilio.accountSid=**********************************
twilio.authToken=********************************
```

* create a service layer for twilio

```java
package com.ums.service;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;
import com.twilio.Twilio;
import com.twilio.rest.api.v2010.account.Message;
import com.twilio.type.PhoneNumber;

@Service
public class TwilioSmsService {

    @Value("${twilio.accountSid}")
    private String ACCOUNT_SID;

    @Value("${twilio.authToken}")
    private String AUTH_TOKEN;

    public void sendSms(String to, String messageBody) {
        Twilio.init(ACCOUNT_SID, AUTH_TOKEN);

        Message message = Message.creator(
                        new PhoneNumber(to),
                        new PhoneNumber("+12198984840"),
                        messageBody)
                .create();

        System.out.println("Message SID: " + message.getSid());
    }
}

```