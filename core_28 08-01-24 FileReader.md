**createNewFile()**
* This is a non-static method present inside file class.
* If file is created this method will return true or else false.

```java
import java.io.File;
import java.io.IOException;

public class A {
	public static void main(String[] args) {
		File f = new File("D://test//A.txt");
		
		try {
			boolean val = f.createNewFile();
			System.out.println(val);
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
**length()**
* This is a non-static method present inside file class.
* This method counts the number of characters including thite spaces and returns long value.
```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("D://test//A.txt");
		
		long val = f.length();
		System.out.println(val);
	}
}
```
**mkdir()**
* This is a non-static method present inside file class.
* This methods will create new folder if the folder doesnot exist.
* If folder is created it will return true or else false.
```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("D://test//p1");
		
		boolean val = f.mkdir();
		System.out.println(val);
	}
}
```

---

```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("D://test//p1");
		
		boolean val = f.delete();
		System.out.println(val);
	}
}
```
**list()**
* This is a non-static method present inside file class.
* This method will return all the file/folder names in the given path as string array.
```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("D://test");
		
		String[] val = f.list();
		
		for (String s : val) {
			System.out.println(s);
		}
	}
}
```
### File reader ###

```java
import java.io.File;
import java.io.FileReader;

public class A {
	public static void main(String[] args) {
		File f = new File("D://test//A.txt");
		try {
			FileReader fr = new FileReader(f);
			for (int i = 0; i < f.length(); i++) {
				System.out.print((char) fr.read());
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```