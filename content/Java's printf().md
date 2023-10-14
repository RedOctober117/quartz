`printf()` provides a more direct way of formatting strings with values only known at run-time. Consider the following comparison of `println()` vs. `printf()`:
```java
public class Tester {
  public static void main(String[] args) {
    Scanner in = new Scanner(System.in);
	System.out.print("Enter a value: ");
	double userInput = in.nextDouble();

	System.out.println("(With println) You entered: " + userInput);
	System.out.printf("(With printf) You entered: %f\n", userInput);
  }
}
```

Let's deconstruct our `printf()`. First and foremost, the method itself is called `printf`, meaning _"print format"_. `printf()` has two distinct behaviors, compared to `println()`:
- `printf()` _does not_ append a new line character automatically
- `printf()` _does_ allow variable substitution

You will notice the lack of a new line pretty quickly if you have anything printed after a `printf()` statement. We can insert our own new line any place we please by using the `%n` or `\n` flag. These flags are equivalent, but "backslash n" is the widely used code, whereas "percent n" is the [[Java]] specific flag. Both are recognized by Java. **Note**: the new line character _must_ be placed **within** the `""`. You will receive a compile error otherwise.

Variable substitution is the second benefit afforded by `printf()`. Here's the basic format:
```java
double variableOfDoubleOrFloatingType = 42;
System.out.printf("%f <- your variable is substituted here!", variableOfDoubleOrFloatingType);
```

To have `printf()` substitute our variable, we must first use the correct `flag`. Each primitive has a corresponding flag built into Java:
- `s` = `String`
- `d` = `int`
- `f` = `float` or `double`
- `t` = `date/time`
- `b` = `boolean`
- `c` = `char`

The format for a flag is as follows:
```txt
%[flags][width][.precision]conversion-character
```

Please visit [Baeldung](https://www.baeldung.com/java-printstream-printf) for a breakdown of each flag.
