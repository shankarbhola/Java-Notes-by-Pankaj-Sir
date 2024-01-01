### enum ###
* enum is collection of constents 
```java
public enum Calender {
	Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec
}

```
```java
public class A {
	public static void main(String[] args) {
		System.out.println(Calender.Oct);
	}
}
```
---
```java
public enum Salutation {
	Mr, Mrs, Dr, Prof
}
```
```java
public class A{
	public static void main(String[] args) {
		System.out.println(Salutation.Mr);
	}
}
```
### Wrapper class ###
* Here the values stored in object 
* The process of storing the value inside an object is called as wrapping or boxing
* Reading the value from the object is called as unboxing
	* byte : Byte
	* short : Short
	* int : Integer
	* long : Long
	* float : Float
	* double : Double
	* char : Character
	* boolean : Boolean
```java
public class A{
	public static void main(String[] args) {
		Integer i  = 10;
		System.out.println(Integer.MAX_VALUE);
		System.out.println(Integer.MIN_VALUE);
		System.out.println(i.longValue());
		System.out.println(i.hashCode());
		System.out.println(i.SIZE);
		System.out.println(i.toString());
		System.out.println(i.doubleValue());
		System.out.println(i.byteValue());
		
		Integer j = new Integer(10);
		
	}
}

```
---
```java
public class A{
	public static void main(String[] args) {

		Byte b = 10;
		Short s =20;
		Integer i = 30;
		Long l = 40L;
		Float f = 10.3F;
		Double d = 10.3;
		Character c = 'a';
		Boolean o = true;
	}
}
```
### finalize() ###
* Finalize is a method presend inside Object class
* Garbag collection logic is implemented in finalize method

```java
public class A extends Object{
	@Override
	protected void finalize(){
		System.out.println(100);
	}
	public static void main(String[] args) {
		A a1 = new A();
		a1 = null;
		System.gc();
	}
}```
