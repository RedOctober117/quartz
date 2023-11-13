_Arrays_ in [[Java]] provide a way to group like-data in a sort-of list. Data is added or removed by its `index`, a number representing the position of an `element`. Arrays in Java (and most languages) begin with an `index` of `0`. 
```java
public class ArrayExample
	public static void main(String[] args) {
		int[] arrayOfIntegers = new int[1];
		arrayOfIntegers[0] = 2;
		System.out.println(arrayOfIntegers[0]);
	}
```

In the above code, we initialize an array `arrayOfIntegers` and set it equal to a `new` integer array `int[]`. Within the brackets of the `new` statement, the size of the array is specified. Array sizes are **immutable** in Java, meaning you cannot increase or decrease the number of `elements` in an array without creating a new array entirely.

Instead of explicitly stating the size of an array with `new int[]`, we can implicitly declare the size by passing in values immediately. The array will then have a size equal to the number of elements first placed inside of it, for the duration of its life.
```java
// cut
int[] implicitIntegerArray = {1, 2, 3};
System.out.println(implicitIntegerArray.length()); // Returns 3
```

Here, we implicitly declared the size of the array as three by passing in three `elements`. 

## Indexes
_Indexes_ of an array are integer values representing the position of a given `element` within an array. In [[Java]], elements begin at `index 0`, thus the index of the final element is the number of elements in the array minus one. 
Array elements can be accessed with the following notation:
```java
someArray[index];
```
This will return a copy of the value at the given index. 