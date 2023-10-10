[[Java]] provides a class `File` to handle file IO. Here is a basic program to print the contents of an input file, and write the contents of an input file to an output file:
```java
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Scanner;

public class Files {
	public static void main(String[] args) throws FileNotFoundException, IOException {
		File f1 = new File("input.txt");
	// System.out.println(f1.getAbsolutePath());
	// System.out.println(f1.getCanonicalPath());
	// File f2 = new File(f1.toPath());
	Scanner in = new Scanner(f1);
		while (in.hasNextLine()){
			System.out.println(in.nextLine());
		}
	}
}
```
_Note that this program does not use try/catch, it just `throws FileNotFoundException, IOException`_.

**IMPORTANT:** If the file path inside `File()` is **relative**, Java will only see that file if `java` is invoked in the same directory as the source file. If our source file `Files.java` is at `/home/user/programs/java/Files.java`, we **must** execute `javac Files.java` and `java Files` inside the `java` directory. If you use VSCode, `java` is **not** executed in the project directory (see the command VSCode runs when you use the play button).
