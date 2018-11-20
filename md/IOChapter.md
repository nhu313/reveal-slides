## Input/Output streams, readers, writers

-
-
### Input/output streams

- Stream - a sequence of data
- Input streams - a source to read bytes
- Output streams - a destination to write bytes
- Not related to the collection Streams API

-
### Input Stream

- Come from multiple sources (eg: files, network, user input)

<img src="https://docs.oracle.com/javase/tutorial/figures/essential/io-ins.gif">

-
### User input stream

```java
InputStream input = System.in;
Scanner scanner = new Scanner(input);
String userInput = scanner.nextLine();
```

-
### File input stream

Reading a file

```java
String filePath = "./src/main/resources/users.csv";
FileInputStream input = new FileInputStream(filePath);
Scanner scanner = new Scanner(input);

StringBuilder builder = new StringBuilder();

while(scanner.hasNextLine()) {
    builder.append(scanner.nextLine() + "\n");
}

```

-
### File input stream

Another way to read a file

```java
String filePath = "./src/main/resources/users.csv";

//You can use Files.newInputStream instead of new FileInputStream
//but you need to give it a Path object, not a string
Path path = Paths.get(filePath);
InputStream input = Files.newInputStream(path);

//get the input stream
Scanner scanner = new Scanner(input);
//set the delimiter to the end of file character
scanner.useDelimiter("\\Z");

//read the whole file until it get to \\Z
//which is the end of the file
String content = scanner.next();

```

-
## Ending character

New line character

- `"\r\n"`
- `"\r"`
- `"\n"`

End of file
- `"\Z"`

[Pattern](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html)

-
## Reading a file

Another way to read a file without stream

```java
byte[] bytes = Files.readAllBytes(Paths.get(filePath));
String content = new String(bytes);
```


-
### Creating Input Streams

- `Files.newInputStream(new Path(filePath))` - read file
- `new URL(urlstring).openStream()` - read network (e.g. website, api) content
- `new ByteArrayInputStream(byteArray)` - read byte

-

### Mocking out user input

We know `System.in` is an input stream

```java
InputStream input = System.in
```

Create the Console class and pass in InputStream.

That way we can mock out the InputStream in the test.

```java
public class Console {
    private Scanner scanner;
    private PrintStream output;

    public Console(InputStream input, PrintStream output) {
        scanner = new Scanner(input);
        this.output = output;
    }

    public String getUserInput(){
        return scanner.nextLine();
    }
}
```

-

### Mocking out user input

Setting up the test

```java
// create the input stream to mock the user input
byte[] bytes = "2\nwords".getBytes();
InputStream input = new ByteInputStream(bytes, bytes.length);

// Create the new console with the mock input stream
Console console = new Console(input, System.out);

// Pass the console to the game
BlackJackGame game = new BlackJackGame(console);

```

The Console class

```java
// because the scanner has our mocked input stream
// when it gets call, it will return the value we set (2, words)
public String getUserInput(){
    return scanner.nextLine();
}
```

-
### Console

In your code

```java
Console console = new Console(System.in, System.out);
BlackJackGame game = new BlackJackGame(console);
```

-
-

## Output Stream

A destination to write data

-
#### Creating Output Streams

- `Files.newOutputStream(path)`
- `URLConnection.getOutputStream()`
- `new ByteArrayOutputStream()`
  - can be converted to `ByteArray` after writing

-
## Output Stream

`System.out` is a PrintStream

```java
PrintStream printStream = System.out;
printStream.print("hello");
```

PrintStream is an OutputStream

```java
OutputStream output = System.out;
//will prints hello to the console
output.write("hello".getBytes());
```

-

## Mocking OutputStream

We know System.out is a PrintStream

```java
PrintStream printStream = System.out;
printStream.print("hello");
```

Make Console take in PrintStream to mock it out

```java
public class Console {
    private Scanner scanner;
    private PrintStream output;

    public Console(InputStream input, PrintStream output) {
        scanner = new Scanner(input);
        this.output = output;
    }

    public void printMessage(String message) {
        this.output.print(message);
    }
}

```

-
## Mocking OutputStream in Test

```java
@Test
public void testWelcomeMessage(){
  //Given - Set up stream
  ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
  PrintStream output = new PrintStream(outputStream);
  //set up game
  Console console = new Console(System.in, output);
  BlackJackGame game = new BlackJackGame(console);

  //when
  game.start();
  String actual = outputStream.toString();

  //Then
  String expected = "Welcome to BlackJack";
  Assert.assertEquals(expected, actual);
}
```

-
## Console

In your code

```java
Console console = new Console(System.in, System.out);
BlackJackGame game = new BlackJackGame(console);
```

-
## File OutputStream

```java
FileOutputStream output = null;
try {
    boolean append = true;
    output = new FileOutputStream("user.csv", append);
    output.write("why111".getBytes());
    output.close();
}finally {
    if (output != null) {
        output.close();
    }
}
```

-

## File OutputStreamWriter
Write to a file using `FileWriter` which has an output stream

```java
OutputStreamWriter fileWriter = null;
try {
    //use new FileWriter() to write to replace the file content
    boolean append = true;
    fileWriter = new FileWriter("testFile.csv", append);

    fileWriter.write("why");
    fileWriter.close();
}finally {
    if (fileWriter != null) {
        // make sure to close the file if it's open
        fileWriter.close();
    }
}
```



-
## Read and write


```java
FileInputStream input = null;
FileOutputStream out = null;

try {
    in = new FileInputStream("users.csv");
    out = new FileOutputStream("copy_users.csv");
    int c;

    while ((c = in.read()) != -1) {
        out.write(c);
    }
} finally {
    if (in != null) {
        in.close();
    }
    if (out != null) {
        out.close();
    }
}
```

-

## Read and write

<img src="https://docs.oracle.com/javase/tutorial/figures/essential/byteStream.gif">

-
-

## Paths

- a route to a file/directory
- can be absolute (`/Users/dee/zcw/labs`)
- can be relative (`labs`)

-
## Get a path

```java
Path path1 = Paths.get("src/main/resources/users.csv");
Path path2 = Paths.get("src", "main", "resources", "users.csv");
Path path3 = Paths.get("src/main/", "resources", "users.csv");
Path path4 = Paths.get("./src/main/", "resources", "users.csv");
```

-
## Resolve a path

```java

Path rootPath = Paths.get("/users/dee/zcw");
// filePath is /users/dee/zcwuser.csv
Path filePath = rootPath.resolve("user.csv");

```

-
-


## URL Connections

-
### Get a URLConnection

Call `openConnection` on a `URL` object eg:

```java
URL url = new URL("http://www.google.com");
URLConnection conn = url.openConnection();
```

-
## Read content

```java
URLConnection conn = url.openConnection();
InputStreamReader inputStream = null;
BufferedReader reader = null;
try {
    inputStream = new InputStreamReader(conn.getInputStream());
    BufferedReader br = new BufferedReader(inputStream);

    String inputLine = null;
    while ((inputLine = br.readLine()) != null) {
        System.out.println(inputLine);
    }
} finally {
    reader.close();
}
```

-
-

### Directory operations

- `Files.createDirectory(path)` -- like `mkdir path`
- `Files.createDirectories(path)` -- like `mkdir -p path`
- `Files.createFile(path)`
- `Files.exists(path)`

-
### File operations

- `Files.copy(fromPath, toPath, options...)`
- `Files.move(fromPath, toPath, options...)`
- `Files.delete(path)`, `Files.deleteIfExists(path)`

[Files API - Options](https://docs.oracle.com/javase/7/docs/api/java/nio/file/Files.html#copy(java.nio.file.Path,%20java.nio.file.Path,%20java.nio.file.CopyOption...)
-
### Viewing directory contents

List out the files/directories

```java
Stream<Path> paths = Files.list("/users/dee/zcw");
```

List out the files/directories and subdirectories

```java
Stream<Path> paths = Files.walk("/users/dee/zcw");
```
-
-
## Zip File Systems

ZIP files are just self-contained filesystems. Access them with the
 `FileSystems` and `FileSystem` classes

-
### Read paths from a ZIP file

```Java
//class loader to find the provider
ClassLoader classLoader = null;
FileSystem fs = FileSystems.newFileSystem(Paths.get("data.zip"), classLoader);
Stream<Path> entries = Files.walk(fs.getPath("/"));
```

-
#### Writing to ZIP archives

```Java
Path zipPath = Paths.get("archive.zip");
URI uri = new URI("jar", zipPath.toUri().toString(), null);
Map<String, String> env = Collections.singletonMap("create", "true");

String fileName = "users.csv";
try (FileSystem fs = FileSystems.newFileSystem(uri, env);){
    Files.copy(Paths.get(fileName), fs.getPath("/").resolve(fileName));
}
```

- env - a map of provider specific properties to configure the file system; may be empty

[FileSystems API](https://docs.oracle.com/javase/7/docs/api/java/nio/file/FileSystems.html)

-
-
## Serialization

Convert Java objects state into Java byte streams

-
## Deserialization

Convert Java byte stream into Java object

-
## Serialization

- a mechanism to persist the object
- Classes must implement `Serializable` to be serialized
- Serialization is safe if all instance variables are primitives, enums, or other Serializable objects
- Collections are Serializable if their elements are.

Note: Shared references to a serialized object must match after deserialization

-
### transient modifier

- marks instance variables that shouldn't be serialized
- Usually used on derived values or non-`Serializable` values

-
#### Example

```Java
public class Student implements Serializable{
  private List<Integer> testScores;
  // calculated from testScores
  private transient GradeStats gradeStats;

  public GradeStats getStats(){
    if(gradeStats == null){
      gradeStats = new GradeStats(testScores);
    }
    return GradeStats;
  }
}
```

-
### Customizing serialization behavior

- Override default serialization behavior with:
  - `readObject(ObjectInputStream in)` and
  - `writeObject(ObjectOutputStream out)`
- prevents automatic serialization of instance variables.
- No need to manage superclass instance variables, only `this`

-
### Full Signatures

general interface for serialization

```Java
// from java.io.ObjectOutputStream:
public final void writeObject(ObjectOutputStream outputStream)
                       throws IOException

// from java.io.ObjectInputStream
public final Object readObject(ObjectInputStream inputStream)
                  throws IOException,  ClassNotFoundException
```

[Serialization's Blog](https://www.oracle.com/technetwork/articles/java/javaserial-1536170.html)
