## Logging

* Logging is an essential aspect of application development that allows developers to monitor and troubleshoot their applications. 
* SLF4J (Simple Logging Facade for Java) is a logging framework that provides a simple abstraction for various logging frameworks like Java Util Logging, Log4j, Logback, etc. In Spring Boot, SLF4J is commonly used to standardize logging across the application.
### **SLF4J in Spring Boot**

#### **What is SLF4J?**
SLF4J (Simple Logging Facade for Java) is a simple abstraction for various logging frameworks, allowing you to switch between different logging implementations (like Logback, Log4j, etc.) without changing your application code.

#### **Why Use SLF4J?**
- **Flexibility**: Allows you to use different logging frameworks.
- **Consistency**: Provides a consistent logging API across various frameworks.
- **Ease of Use**: Simplifies the process of logging in your application.

### **Setting Up SLF4J in Spring Boot**

#### **1. Dependencies**
Spring Boot includes SLF4J and Logback by default, so you usually don't need to add them manually. If needed, include these dependencies in your `pom.xml` for a Maven project:

```xml
<dependencies>
    <!-- SLF4J API -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.36</version>
    </dependency>
    <!-- Logback Classic -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.10</version>
    </dependency>
</dependencies>
```

#### **2. Basic Usage**

**Import SLF4J Logger:**
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
```

**Create a Logger Instance:**
```java
private static final Logger logger = LoggerFactory.getLogger(YourClassName.class);
```

**Log Messages:**
```java
logger.info("This is an info message");
logger.debug("This is a debug message");
logger.error("This is an error message");
```

### **Configuring Logging with application.properties**

**Specify Log File Location:**
```properties
logging.file.name=logs/application.log
```

**Set Logging Levels:**
```properties
logging.level.root=INFO
logging.level.com.yourpackage=DEBUG
```

**Define Logging Patterns:**
```properties
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %msg%n
logging.pattern.file=%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
```

### **Example Configuration in application.properties**
```properties
# Log file location
logging.file.name=logs/application.log

# Logging levels
logging.level.root=INFO
logging.level.com.example=DEBUG

# Logging patterns
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %msg%n
logging.pattern.file=%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
```

### **Accessing Log Files**

- **Local Development**: Navigate to the `logs` directory in your project folder to find `application.log`.
- **Real-Time Viewing**: Use tools like `tail` on Unix-based systems to view logs in real-time:
  ```sh
  tail -f logs/application.log
  ```

### **Example Code with Logging**

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    private static final Logger logger = LoggerFactory.getLogger(MyController.class);

    @GetMapping("/log")
    public String logExample() {
        logger.info("Info log message");
        logger.debug("Debug log message");
        logger.error("Error log message");
        return "Check the logs for messages";
    }
}
```

### **Summary**

1. **Add Dependencies**: Ensure SLF4J and Logback are included.
2. **Configure Logging**: Use `application.properties` for basic configuration.
3. **Log Messages**: Use SLF4J's `Logger` to log messages at various levels.
4. **Access Logs**: Find logs in the specified log file location and view them using tools like `tail`.

By following these steps, you can effectively implement and manage logging in your Spring Boot application using SLF4J.
