#Java 
A loop is a part of a program that runs repeatedly until a desired condition is met. 

[[For]]
[[For#Enhanced For Loop]]
[[While]]
[[Do]]
[[Do While]]


# Do
# Do While
```java
do {
     statement(s)
} 
while (expression);
```

# For-Each Array Loop
```java
for (_arrayDataType_ _variable_ : _arrayName_){
	statement;
}
```
# Applications

```
## For

## Do

## For-Each Array Loop
```java
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (String i : cars) {
  System.out.println(i);
}

// Loop to create objects on demand
ArrayList<_dataType_>() _arrayName_ = new ArrayList<_dataType_>();
Scanner in = new Scanner(System.in);
for(_dataType_ _var_ : _arrayName_){
	// ask for input
	_dataType_ _varName_ = in.next_dataType_();
	
}
```