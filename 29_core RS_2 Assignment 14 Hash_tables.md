## Hash code ##
![picture](https://i.ibb.co/wKpYxGk/image.png)

```java
public class A {
    public static void main(String args[]) {
      String x = "Mia";
      System.out.println(x.hashCode());
    }
}
```
* hashing is the technique where we are representing any entity in the form of integer and it is done in java using a hashcode method
* hashcode is a method present inside object class in java
* hash table is an associated array
* where the values are stored as a key value pair

**collision**
* When 2 values are being store at the same index number its called as collision
* to solve this problem in hash table we store the data as a list maped to the same index number
