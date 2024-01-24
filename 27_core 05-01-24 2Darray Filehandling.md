### 2D Array ###

```java
public class A {
	public static void main(String[] args) {
		int[][] x = new int[3][3];
		x[0][0]=10;
		x[0][1]=20;
		x[0][2]=30;
		x[1][0]=40;
		x[1][1]=50;
		x[1][2]=60;
		x[2][0]=70;
		x[2][1]=80;
		x[2][2]=90;
		
		for (int i = 0; i < x.length; i++) {
			for (int j = 0; j < x[0].length; j++) {
				System.out.println(x[i][j]);
			}
		}
	}
}

```

# File Handling #

**File
FileReader
FileWriter
BufferedReader
BufferedWriter
FileInputStream**

### File ###

```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("E://reports//A.txt");
		
		System.out.println(f);
	}
}
```
**exist()**
* This is a nonstatic method present in file class.
* It checks whether the file exist in given path .
* If yes it return boolean value true or if does not exist then it will return false.

```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("E://reports//A.txt");
		boolean val = f.exists();
		System.out.println(val);
	}
}

```
**delete()**
* This is a nonstatic method present in file class.
* If the file deleted then it return boolean value true or else it will false false.

```java
import java.io.File;

public class A {
	public static void main(String[] args) {
		File f = new File("E://reports//A.txt");
		boolean val = f.delete();
		System.out.println(val);
	}
}
``` 