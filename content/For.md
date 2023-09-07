# Definition

A `for` loop runs for a specified number of cycles, either denoted by a variable or implicitly by the size of the array.
```java
for (_dataType_ _counter_ = _value_; _counter_ <= _guardian_; _counter__increment_){
	statement executed each time;
}
```
For loops headers are comprised of three main parts:
- The starting bound `_value_`
- The ending bound `_guardian_`
- The value by which we want to increase the `_counter_`, `_increment_`

This can be read as: "For each `_dataType_` `_counter_` incremented by `_increment_`, do something." Consider the following loop:
```java
for (int i = 0; i < ourMaxValue; i++){
	System.out.println(i);
}
```
This can be read as: "For each `int` `i` incremented by `1`, print `i`."

_See: [[#Applications#For Loop]]_

## Enhanced For Loop

Also referred to as a `For-Each` loop, an enhanced for loop is designed for use with arrays.
```java
for (_arrayDataType_ _variable_ : _arrayName_){
	statement;
}
```
For loops can be read as: "For each `_arrayDataType_` `_variable_` of `_arrayName_`, do something." Consider the following loop:
```java
for (Person p : personsArray) {
	System.out.println(p.getName());
}
```
This can be read as: "For each `Person` `p` of the `personsArray` array, print `p.getName()`."

_See: [[#Applications#Enhanced For Loop]]_

# Applications

## For Loop
```java
int[] ints = { 1, 2, 3, 4 };

int sumOfInts = 0;

for (int i = 0; i < ints.length; i++) {
	sumOfInts += ints[i];
}

System.out.println(sumOfInts);

/* Output:
	10
*/
```

## Enhanced For Loop
```java
// Define your array
ArrayList<Integer> intArray = new ArrayList<>();

ints.add(1);
ints.add(2);
ints.add(3);

for (Integer i : intArray){
	System.out.println(intArray.get(i - 1)); 
}

/* Output:
	1
	2
	3
*/
```
Note that in the above code, we subtract `1` from `i` to prevent out of bounds errors. Had we left it as `intArray.get(i)`, we would receive the following output:
```bash
2
3
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3
        at java.base/jdk.internal.util.Preconditions.outOfBounds(Preconditions.java:64)
        at java.base/jdk.internal.util.Preconditions.outOfBoundsCheckIndex(Preconditions.java:70)
        at java.base/jdk.internal.util.Preconditions.checkIndex(Preconditions.java:266)
        at java.base/java.util.Objects.checkIndex(Objects.java:361)
        at java.base/java.util.ArrayList.get(ArrayList.java:427)
        at TestBed.main(TestBed.java:16) 
```
This code returns an error because `i` begins iterating at an index of `1`. Therefore, when it attempts to execute `intArray.get(3)`, it crashes. There is no value in the third index; the array only contains values for indexes `0`, `1`, and `2`.
