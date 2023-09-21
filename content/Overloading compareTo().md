When calling `Collections.sort()`, `compareTo()` is implicitly called as well. To override `compareTo()`, do the following:
```java
@Override
public int compareTo(<Object> o){
	if(this.var > o.getVar()){
		return 1;
	} else if(this.var < o.getVar()) {
		return -1;
	} else {
		return 0;
	}
}
```

The values `1`, `-1`, and `0`, are all used by the `Collections.sort()` method to determine where to put elements of an ArrayList.