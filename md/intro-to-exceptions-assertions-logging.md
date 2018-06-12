###Exceptions, Assertions, Logging
<p class="fragment fade-up">1. Throwable Class</p>
<p class="fragment fade-up">2. Basic Exception Handling</p>
<p class="fragment fade-up">3. Better Exception Handling</p>
<p class="fragment fade-up">4. Finally Keyword</p>
<p class="fragment fade-up">5. Assertions</p>
<p class="fragment fade-up">6. Logging</p>

-
-

###Throwable Hierarchy
<img src = 'https://lh5.googleusercontent.com/WqqNoyFEkZXfmZBBQjgIutY72_BUV6_By_BAe7Ih9u36HfelS3nTWQEYtdRUkQS32Tuhg9P9CUXo-jgvOpkO84vLm2viI4Od0BNustwONdMm7DKZnKC6kyVHyRJbsESLIPV4uBU'>

-
###Errors
<p class="fragment fade-up">* The `Error` hierarchy describes internal errors and resource exhaustion situations.</p>
<p class="fragment fade-up">* Do not advertise (throw) internal java errors. Any code can potentially throw an `Error`.</p>

-
###Errors
#### Common Errors:
<p class="fragment fade-up"> `IOError` - serious I/O error has occurred</p>
<p class="fragment fade-up"> `StackOverflowError` - application recurses too deeply</p>
<p class="fragment fade-up"> `OutOfMemoryError` - JVM cannot allocate an object because it is out of memory</p>

-

###Throwable Hierarchy
<img src = 'https://lh5.googleusercontent.com/WqqNoyFEkZXfmZBBQjgIutY72_BUV6_By_BAe7Ih9u36HfelS3nTWQEYtdRUkQS32Tuhg9P9CUXo-jgvOpkO84vLm2viI4Od0BNustwONdMm7DKZnKC6kyVHyRJbsESLIPV4uBU'>

-
###Unchecked Exceptions
<p class="fragment fade-up">* Any exception which derives from `Error` or `RuntimeException` class.</p>
<p class="fragment fade-up">* An Exception subclassing `RuntimeException` is considered to be the programmer's fault.</p>

-
###Unchecked Exceptions

1. `ArrayIndexOutOfBoundException` can be avoided by testing array index against array bounds
2. `NullPointerException` can be avoided by testing for null values


-
###Checked Exceptions
An Exception subclassing `IOException` is _potentially_ not the programmer's fault.
1. `FileNotFoundException` can be thrown when trying to read from a remote file that a person incidentally removes.
2. `SQLException` can be thrown as a result of a faulty network connection.














-
-
###Basic Exception Handling
* What is Exception Handling?
* Unhandled Exception Example
* Handled Exception Example


-
###What is Exception Handling?
<p class="fragment fade-up">* For exceptional situations, Java uses a form of error trapping called, _exception handling_.</p>
<p class="fragment fade-up">* Exception handling enables the author of the code to record and handle errors in their program.</p>

-
###<strike>Unchecked</strike> Unhandled Exception Example: Compile Error
```java
import java.io.*;
class FilePrinter {
    private final BufferedReader reader;

    public FilePrinter(String fileDirectory) {
		// What if the file does not exist?
		this.reader = new BufferedReader(new FileReader(fileDirectory));
    }

    public void printFile() {
        String line = null;
        do {
            // What if the System fails to read in the next line?
            // (For example if the file was suddenly closed, modified, or deleted)
            line = reader.readLine();
            System.out.println(line);
        } while (line != null);
    }
}
```

-
###Exception Handling: Signature Throw Clause
```java
import java.io.*;
class FilePrinter {
    private final BufferedReader reader;

    public FilePrinter(String fileDirectory) throws FileNotFoundException {
        this.reader = new BufferedReader(new FileReader(fileDirectory));
    }

    public void printFile() throws IOException {
        String line = null;
        do {
            line = reader.readLine();
            System.out.println(line);
        } while (line != null);
    }
}
```

-
###Exception Handling: Try / Catch
```java
import java.io.*;
class FilePrinter {
    private final BufferedReader reader;

    public void printFile() {
        String line = null;
        try {
          do {
              line = reader.readLine();
              System.out.println(line);
          } while (line != null);
        } catch (IOException e) {
          e.printStackTrace();
        }
    }

    public FilePrinter(String fileDirectory) throws FileNotFoundException {
        this.reader = new BufferedReader(new FileReader(fileDirectory));
    }
}
```

-
### Catching Multiple Exceptions

```java
public void readFile()  {
    FilePrinter fpt = null;
    try {
      fpt = new FilePrinter("bad file name");
      fpt.printFile();
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (NullPointerException e ) {
        e.printStackTrace();
    }
}
```

-
### Catching Multiple Exceptions

```Java   
public class FilePrinterTest {
	public void testInstantiateAndPrint() {
	    FilePrinter fpt = null;
	    try {
	        fpt = new FilePrinter("bad file name");
	        fpt.printFile();
	    // bit-wise operator supported by java 1.7+    
	    } catch(FileNotFoundException | NullPointerException exception) {
	        exception.printStackTrace();
	    }
	}
}
```

-
### Catching Multiple Exceptions

```java
public void readFile()  {
    FilePrinter fpt = null;
    try {
      fpt = new FilePrinter("bad file name");
      fpt.printFile();
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (IOException e ) {
        e.printStackTrace();
    }
}
```

-
### Catching Multiple Exceptions

Cannot do this because FileNotFoundException is a subclass of IOException.
Since they do the same thing, there is no need to catch FileNotFoundException.

```Java   
public class FilePrinterTest {
	public void testInstantiateAndPrint() {
	    FilePrinter fpt = null;
	    try {
	        fpt = new FilePrinter("bad file name");
	        fpt.printFile();
	    // bit-wise operator supported by java 1.7+    
	    } catch(FileNotFoundException | IOException exception) {
	        exception.printStackTrace();
	    }
	}
}
```
-

###Throwable Hierarchy
<img src = 'https://lh5.googleusercontent.com/WqqNoyFEkZXfmZBBQjgIutY72_BUV6_By_BAe7Ih9u36HfelS3nTWQEYtdRUkQS32Tuhg9P9CUXo-jgvOpkO84vLm2viI4Od0BNustwONdMm7DKZnKC6kyVHyRJbsESLIPV4uBU'>

-
### Catching Multiple Exceptions

Catch IOException will also handle FileNotFoundException

```Java   
public class FilePrinterTest {
	public void testInstantiateAndPrint() {
	    FilePrinter fpt = null;
	    try {
	        fpt = new FilePrinter("bad file name");
	        fpt.printFile();
	    // bit-wise operator supported by java 1.7+    
	    } catch(IOException exception) {
	        exception.printStackTrace();
	    }
	}
}
```
-
###Recursion <strike>and</strike> Exception Handling
<p class="fragment fade-up">* DON'T DO IT!</p>
<p class="fragment fade-up">* Recursion and Exception Handling do not go together</p>
<p class="fragment fade-up">* Exceptions keep track of all pending method calls</p>
<p class="fragment fade-up">* By nature, recursion pends method calls `n` levels deep, where `n` is the recursive depth of the method call.</p>
<p class="fragment fade-up">* Combining recursion and exception handling can result in very strange `StackTraces`</p>

-
-
###Finally Keyword
<p class="fragment fade-up">* When code throws an exception, it stops processing the remaining code in the scope, then exits the method.</p>
<p class="fragment fade-up">* If the method has acquired some local resource, then this can become an issue; The program will cease execution, and hold the resource indefinitely.</p>
<p class="fragment fade-up">* The finally clause executes whether or not an exception was caught.</p>

-
###Conditions under which `finally` block is executed
<p class="fragment fade-up">1. If no exception are thrown.</p>
<p class="fragment fade-up">2. If exception outside `try` block is thrown.</p>
<p class="fragment fade-up">3. If an exception is thrown in a `catch` clause.</p>
<p class="fragment fade-up">4. The program skips the `finally` clause, if the `catch` clause does not throw an exception.</p>


-

###Finally Keyword


```Java   
class BookExample {
	public void example1() {
		InputStream in = ... ; //open a file
		try {
				// code that may throw exception
		} catch(IOException ioe) {
			/// handle exception some way
		} finally {
          in.close();
        }
	}
}
```

-
-
### Testing

```java
@Test(expected = FileNotFoundException.class)
public void testThrowException() throws FileNotFoundException {
    FilePrinter printer = new FilePrinter("bad file name");
}
```

-
-
### Catching exception
* Catch exception you can handle
* Throw exception you can't

-
- Exception handling should not be replaced by a check (null/index out of bound)
- Do not micromanage exception (don't catch multiple low level exception when you don't have to)
- Make good use of the exception hierarchy (find the appropriate subclass to thow)
- Do not squelch exceptions
- Propagating exceptions is not a sign of shame


-
-
###Assertions

```java
if (x < 0) throw new IllegalArgumentException("x < 0");
```

Use assert:

```java
assert x >= 0;
```

Or with a message
```java
assert x >= 0 : "number can't be negative";
```

-
###Assertions
<p class="fragment fade-up">* Assertions are commonly used idiom of defensive programming.</p>
<p class="fragment fade-up">* Java has a keyword `assert`, which takes two forms:</p>
	<p class="fragment fade-up">1. `assert condition;`</p>
	<p class="fragment fade-up">2. `assert condition : expression;`</p>
<p class="fragment fade-up">* `assert` evaluates a condition, then throws an `AssertionError` if it is false. The second argument _expression_ is a message String.</p>


-
###Toggling Assert Statements
<p class="fragment fade-up">* By default, assertions are disabled; If an assert statement is passed `false`, no exception is thrown.</p>
<p class="fragment fade-up">* Assertions can be enabled by running the program with the `-ea` option.</p>
<p class="fragment fade-up">* `java -ea MyProject` enables for entire project</p>
<p class="fragment fade-up">* `java -ea:MyClass -ea:com.zipcodewilmington.MyProject` enables for `MyClass`</p>

-
###When To Use
<p class="fragment fade-up">* Assertion failures are intended to be fatal, unrecoverable errors</p>
<p class="fragment fade-up">* Assertion checks are turned on only during development and testing</p>
<p class="fragment fade-up">* As an additional check against uncanny method returns.</p>


-
-
###Logging
<p class="fragment fade-up">* It's common to use `System.out.println` to check against troublesome code.</p>
<p class="fragment fade-up">* Once the issue is resolved, these statements are usually removed, or commented out.</p>
<p class="fragment fade-up">* Later, if the issue persists, the print statements are re-inserted.</p>
<p class="fragment fade-up">* The Logging API is designed to overcome this issue.</p>

-
###Principal advantages of Logging API
<p class="fragment fade-up">* It's easy to (un)suppress all log records, or just those below a certain level.</p>
<p class="fragment fade-up">* Suppressed logs are inexpensive; The penalty for leaving them in your code is minimal.</p>
<p class="fragment fade-up">* Log records can be directed to different handlers; Console display, writing to file / database, etc.</p>
<p class="fragment fade-up">* Log records can be formatted; For example: plain text, or XML</p>
<p class="fragment fade-up">* Logging configuration is controlled by configuration file; Applications can replace this mechanism</p>



-
###The 7 Logging Levels
* By default, loggers will log all messages of `INFO` or higher to console.
* `SEVERE` highest
* `WARNING`
* `INFO` default
* `CONFIG`
* `FINE`
* `FINER`
* `FINEST` lowest

-
###Syntax
```
public class LogDemo {
	 // it is advised that you name your logger the same as your Main Application package
    Logger logger = Logger.getLogger("com.zipcodewilmington.MainApplication");
    public void logTest() {
        logger.setLevel(Level.SEVERE);  // log severe
        logger.setLevel(Level.WARNING); // log severe, warning
        logger.setLevel(Level.INFO);    // log severe, warning, info
        logger.setLevel(Level.CONFIG);  // log severe, warning, info, config
        logger.setLevel(Level.FINE);    // log severe, warning, info, config, fine
        logger.setLevel(Level.FINER);   // log severe, warning, info, config, fine, finer
        logger.setLevel(Level.FINEST);  // log severe, warning, info, config, fine, finer, finest
    }
}
```
-
<img src = 'https://i.pinimg.com/originals/f7/1e/7c/f71e7c464445db9da347def01636a281.jpg'>
