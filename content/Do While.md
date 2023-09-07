# Definition

A `do while` [[Loops|loop]] performs some action while a condition is true. This differs from a [[While|while]] loop because the condition is checked after execution, not before, and the loop will always run at least once. 
```java
do {
     statement(s)
} 
while (_conditionMet_);
```
This is quite simply read as "`Do` something `while` `_conditionMet_`." Consider the following loop:
```java
int counter = 0;
boolean done = false;

do {
	for (int i = 0; i < 5; i++) {
		System.out.println(counter);
		counter++;
	}
	
	done = true;
	System.out.println("Done!");
} while (!done);
```
We receive the following:
```txt
0
1
2
3
4
Done!
```
If instead we defined `done = true`, we would still receive the same output because the statement is always run at least once.

# Applications