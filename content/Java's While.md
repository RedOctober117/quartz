# Definition

A `while` [[Loops|loop]] runs _while_ a condition is met.
```java
// Define a variable to use as a stopping mechanism
boolean _condition_ = false;

while(_conditionMet_){
	statement until condition met, where done = false;
}
```
While loops are read much easier than [[Java's For|for loops]]. "While `_conditionMet_` is true, do something." This can be a little wonky at the beginning, but it's important to remember that while loops only run while something is **true**. The logic to flip that switch to false will be inside the loop itself. 

An intuitive example of this is as follows:
```java
boolean done = false;

while (!done){
	for (int i = 0; i < 5; i++){
		System.out.println("Not done yet!");
	}
	done = true;
}
```
We receive the following output: 
```txt
Not done yet!
Not done yet!
Not done yet!
Not done yet!
Not done yet!
Done!
```
So, while we are _not_ done (`!done`), we print "`Not done yet!`", and after five cycles, we set `done = true` and terminate the loop.

_See: [[#Applications]]_.
# Applications
```java
public class experiment{
  public static void main(String[] args){
    int year = 0;
    double balance = 1000;
    double interest = .05;
    
    while (balance < 10000){
	    year ++;
	    balance = (balance * interest) + balance;
    }
    
    System.out.printf("It took %d years to generate $%8.2f from interest.", year, balance);
  }
}
```
## Print all squares less than n
```java
import java.lang.Math;

public class experiment{
  public static void main(String[] args){
    int upperBound = 100;
    int initial = 1;
    while (Math.pow(initial,2) < upperBound){
      if (Math.pow(initial, 2) % initial == 0){
        System.out.println(Math.pow(initial,2));
        initial ++;
      } else {
        initial ++;
      }
    }
  }
}

OR

import java.lang.Math;

public class experiment{
  public static void main(String[] args){
    int upperBound = 100;
    int initial = 0;
    while (Math.pow(initial,2) < upperBound){
        System.out.println(Math.pow(initial,2));
        initial ++;
    }
  }
}
```
**Output:**
```java
1.0
4.0
9.0
16.0
25.0
36.0
49.0
64.0
81.0
```
## Print all values less than n evenly divisible by 10
```java
public class experiment{
  public static void main(String[] args){
    int n = 100;
    int divisor = 10;
    int initial = 1;
    while (initial < n){
      if(initial % divisor == 0){
        System.out.println(initial);
        initial ++;
      } else {
        initial ++;
      }
    }
  }
}
```
**Output:**
```java
0
10
20
30
40
50
60
70
80
90
```