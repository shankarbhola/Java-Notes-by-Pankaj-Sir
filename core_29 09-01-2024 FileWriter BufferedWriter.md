```java
import java.io.File;
import java.io.FileReader;

public class A {
	public static void main(String[] args) {
		try {
			File f = new File("D://test//A.txt");
			FileReader fr = new FileReader(f);
			char[] ch = new char[(int)f.length()];
			fr.read(ch);
			for (char c : ch) {
				System.out.print(c);
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
### FileWriter() ###

```java
import java.io.FileWriter;
import java.io.IOException;

public class A {
	public static void main(String[] args) {
		try {
			FileWriter fw = new FileWriter("D://test//A.txt",true);
			
			fw.write(100);
			fw.write("\n");
			fw.write("mike");
			char[] x = {'a', 'b'};
			fw.write(x);
			
			fw.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```

### BufferedWriter() ###

* BufferedWriter() will improve file writer.
* BufferedWriter() will has new line method.
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class A {
	public static void main(String[] args) {
		FileWriter fw;
		try {
			fw = new FileWriter("D://test//A.txt");
			BufferedWriter bw = new BufferedWriter(fw);
			bw.write(100);
			bw.newLine();
			bw.write("mike");
			bw.newLine();
			char[] x = {'a', 'b'};
			bw.write(x);
			bw.close(); // Save & close			
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}
```

### BufferedReader() ###
* It improves file reading performance.
* It has readline() method which can read content line by line.

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class A {
	 public static void main(String[] args) {
		 try {
			FileReader fr = new FileReader("D://test//A.txt");
			 BufferedReader br = new BufferedReader(fr);
			 System.out.println(br.readLine());
			 System.out.println(br.readLine());
			 System.out.println(br.readLine());
			 
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
---
```java
import java.io.BufferedReader;
import java.io.FileReader;

public class A {
	 public static void main(String[] args) {
		 try {
			FileReader fr = new FileReader("D://test//A.txt");
			 BufferedReader br = new BufferedReader(fr);
			 String line;
			 while ((line = br.readLine()) != null) {
				 System.out.println(line);
			}
			 
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```