#Java 

See: [Java SE 8 Documentation](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html)

Scanner is a class that allows for reading input from the user.

`import java.util.Scanner;`

```java
Scanner _objName_ = new Scanner(System.in);
_dataType_ _varName_ = _objName_.next_DataType_();
```

# Methods

## next\[dataType\]
`scanner_object.next[dataType]` returns the corresponding value from the input. Below is an example of a program to take an integer from the user:
```java
import java.util.Scanner;

public class Tester {
	public static void main(String[] args){
		Scanner in = new Scanner(System.in);
		System.out.print("Enter a value please: ");
		int userInput = in.nextInt();

		System.out.println("You entered %d", userInput);
	}
}
```

## hasNext\[dataType\]
Will return `true` as long as the next input has the same _dataType_.

```java
File f1 = new File("input.txt");
Scanner in = new Scanner(f1);
while(f1.hasNextLine()){
	System.out.println(f1.nextLine());
}
```


---
# Examples
## Grading System
```java
import java.util.Scanner;

public class GradingSystem{
	public static void main(String[] args){
		Scanner in = new Scanner(System.in);
		double grade = in.nextDouble();
	}
}
```
For a full use of this example, see [[Decisions#Grading System]]

## Counting while provided input
```java
Scanner in = new Scanner(system.in);
int total = 0;
while (in.hasNextInt()){
	int number  = in.nextInt();
	total += number;
}
```
