**Exception handling**
**Method-1**
```java
@DeleteMapping
public ResponseEntity<String> delete(@RequestParam long id) {
    Optional<Registration> byId = registrationRepository.findById(id);
    if (byId.isPresent()) {
        registrationRepository.deleteById(id);
        return new ResponseEntity<>("Registration Deleted", HttpStatus.OK);
    } else {
        return new ResponseEntity<>("Could not Deleted", HttpStatus.BAD_REQUEST);
    }
}
```
**Method-2**
* Create a new package ```com.webapp.exception```
* Inside this package create a class ```ResourceNotFound```
```java
package com.webapp.exception;

public class ResourceNotFound extends Exception {

}
```
```java
@DeleteMapping
public ResponseEntity<String> delete(@RequestParam long id) {
    Optional<Registration> byId = registrationRepository.findById(id);
    if (byId.isPresent()) {
        registrationRepository.deleteById(id);
    } else {
        try {
            throw new ResourceNotFound();
        } catch (Exception e) {
            return new ResponseEntity<>("Could not Deleted", HttpStatus.BAD_REQUEST);
        }
    }
    return new ResponseEntity<>("Registration Deleted", HttpStatus.OK);
}
```

Functional interface
-
Functional interfaces are interfaces in Java that contain exactly one abstract method. They are extensively used in Java's functional programming paradigm, particularly with lambda expressions and method references. Here are some common types of functional interfaces in Java:

1. **Consumer**: Represents an operation that accepts a single input argument and returns no result. Its functional method is `accept(T t)`.

2. **Supplier**: Represents a supplier of results. It has no input arguments and provides a result via its functional method `get()`.

3. **Predicate**: Represents a predicate (boolean-valued function) of one argument. It provides a test method `test(T t)`.

4. **Function**: Represents a function that accepts one argument and produces a result. It has a method `apply(T t)`.

5. **UnaryOperator**: Represents an operation on a single operand that produces a result of the same type as its operand. It extends `Function` and provides a method `apply(T t)`.

6. **BinaryOperator**: Represents an operation upon two operands of the same type, producing a result of the same type as the operands. It extends `BiFunction` and provides a method `apply(T t1, T t2)`.

7. **BiFunction**: Represents a function that accepts two arguments and produces a result. It provides a method `apply(T t, U u)`.

8. **BiConsumer**: Represents an operation that accepts two input arguments and returns no result. Its functional method is `accept(T t, U u)`.

9. **Runnable**: Represents a task that can be run. It has no input arguments and no return value. Its functional method is `run()`.

10. **Callable**: Represents a task that returns a result and might throw an exception. Its functional method is `call()`.

11. **Comparator**: Represents a comparison function that can be used to compare objects. Its functional method is `compare(T o1, T o2)`.

12. **Runnable**: Represents a task that can be executed concurrently. Its functional method is `run()`.

These functional interfaces are part of the `java.util.function` package in Java. They provide a way to pass functions as arguments, enabling a more functional style of programming in Java.

**Predicate**
```java
package com.webapp;
//Predicate-It takes one input and produces boolean value output
import java.util.function.Predicate;

public class A {
	public static void main(String[] args) {
		Predicate<Integer> val = x->x%2==0;
		boolean result = val.test(10);
		System.out.println(result);
	}
}
```
