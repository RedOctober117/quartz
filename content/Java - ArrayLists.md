_ArrayLists_ provide a number of benefits over standard [[Java - Arrays|arrays]]. Most importantly, they are dynamically sized. Recall that with arrays, once the size is specified, it cannot be changed directly. ArrayLists allow for dynamic addition and removal of elements via the `add()` and `remove()` methods. 

ArrayLists are not part of the `java.lang` library and thus must be imported manually:
```java
import java.util.ArrayList;
```
Once imported, we can begin creating and manipulating ArrayLists:
```java title="_Figure 1.0f_"{1,5}
import java.util.ArrayList;

public class ArrayExample {
	public static void main(String[] args) {
		ArrayList<String> myList = new ArrayList<String>();
	}
}
```
As with any variable, we have declared the **data type**, `ArrayList<String>`, the **variable name**, `myList`, and the **value** it is assigned, `new ArrayList<String>()`.

We have successfully created an ArrayList via its **constructor**, `new ArrayList<>()`. The following line is valid and equivalent to line 5 of _1.0f_:
```java title="_Figure 1.1f_"
ArrayList<String> myList = new ArrayList<>();
```
