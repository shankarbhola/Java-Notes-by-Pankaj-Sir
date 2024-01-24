### Remove duplicate item from array ###
```java
public class A {
	public static void main(String[] args) {
		int[] x = {1,1,2,2,3,4};
		int[] temp = new int[x.length];
		int j =0;
		for (int i = 0; i < x.length-1; i++) {
			if(x[i] != x[i+1]) {
				temp[j] = x[i];
				j++;
			}
		}
		temp[j] = x[x.length-1];
		for (int z : temp) {
			System.out.println(z);
		}
	}
}
```
**Remove zeros**
```java
public class A {
	public static void main(String[] args) {
		int[] x = {1,1,2,2,3,4,5};
		int[] temp = new int[x.length];
		int j =0;
		for (int i = 0; i < x.length-1; i++) {
			if(x[i] != x[i+1]) {
				temp[j] = x[i];
				j++;
			}
		}
		temp[j] = x[x.length-1];

		System.out.println(j);
		
		for (int i = 0; i <= j; i++) {
			System.out.println(temp[i]);
		}
	}
}
```
### Nested Loop ###
```java
public class A {
	public static void main(String[] args) {
		for (int i = 0; i < 5; i++) {
			System.out.println("i:"+i);
			for (int j = 0; j < 5; j++) {
				System.out.println("j:"+j);
			}
		}
	}
}
```
### Array Sorting ###
![picture](https://i.ibb.co/8DsrRbb/26-1.png)

<hr>

**Round 1**

![picture](https://i.ibb.co/JHY02X2/26-2.png)


![picture](https://i.ibb.co/6R5sLPf/26-3.png)


![picture](https://i.ibb.co/711gyxy/26-4.png)

![picture](https://i.ibb.co/nn8f0tJ/26-5.png)

**Round 2**

![picture](https://i.ibb.co/D9Pdg57/26-6.png)

**Round 3**

![picture](https://i.ibb.co/84L1c83/26-7.png)

**Round 4**

![picture](https://i.ibb.co/j4XBtz1/26-8.png)


```java
public class A {
	public static void main(String[] args) {
		int[] x = { 23, 32, 14, 38, 7 };
		int temp = 0;
		for (int j = 0; j < x.length - 1; j++) {
			for (int i = 0; i < x.length - 1; i++) {
				if (x[i] > x[i + 1]) {
					temp = x[i + 1];
					x[i + 1] = x[i];
					x[i] = temp;
				}
			}
		}
		for (int i : x) {
			System.out.println(i);
		}
	}
}
```
**using while loop**
```java
public class A {
	public static void main(String[] args) {
		int[] x = { 23, 32, 14, 38, 7 };
		int temp = 0;
		int i=0;
		int j=0;
		while (j<x.length-1) {
			while (i < x.length-1) {
				if (x[i] > x[i+1]) {
					temp = x[i+1];
					x[i+1] = x[i];
					x[i] = temp;
				}
				i++;
			}
			i=0;
			j++;
		}
		for (int z : x) {
			System.out.println(z);
		}
		
	}
}
```
