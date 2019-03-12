## Reflection

-
### Private

Remember when we said no one can access private methods/fields?

```java
class User {
  private String name;
}
```

<p class="fragment fade-in-then-semi-out">We lied!</p>
<p class="fragment fade-in-then-semi-out">We can use `java.lang.reflect` library to access everything.</p>

-
## The Class Object

Contains info about classes

```java
//get class from a class
Class aclass = String.class;

//get class from an instance
Class bclass = "words".getClass();
```

-
## The Class Object - Field

Given this `User` class

```java
public class User {
    private String firstName;
    private String lastName;
}

```

Get all the declared fields with `getDeclaredFields`
```java
//import java.lang.reflect.Field;

Class aclass = User.class;
//get all the field for that class
Field[] fields = aclass.getDeclaredFields();

for (Field field : fields) {
  //prints out all the field name including the private ones
  System.out.println(field.getName());
}
```

User `getFields` to get the public fields

-
## The Class Object

```java
public class User {
    private String firstName;
    private String lastName;
}

```
Set field

```java
//create an instance of the user
User user = new User("Grace", "Hopper");

//get the class
Class aclass = user.getClass();

//get the field
Field fieldName = aclass.getDeclaredField("lastName");

//because the field is private, we have to setAccessible to true
fieldName.setAccessible(true);

//change the user last name to Liskov
fieldName.set(user, "Liskov");
```

-
## The Class Object
`.newInstance()` - for an empty constructor

```java
package com.zipcoder.cohort5;

public class User {
    private String firstName;
    private String lastName;
}
```

Create a new instance base on the class name

```java
//given the full class name
String fullClassName = "com.zipcoder.cohort5.User";

//get the class
Class aClass = Class.forName(fullClassName);

//create a new instance
Object user = aClass.newInstance();
```
-

## The Class Object - Constructor

```java
package com.zipcoder.cohort5;

public class User {
    private String firstName;
    private String lastName;

    public User(String firstName, String lastName) {
      this.firstName = firstName;
      this.lastName = lastName;
    }
}
```

Create a new instance with params for one constructor

```java
Constructor[] constructors = aClass.getConstructors();
Constructor constructor = constructors[0];
Object user = constructor.newInstance("Grace", "Hopper");
```

-

## The Class Object - Constructor
For multiple constructors, declare the argument types

```java
public User(){}

public User(String firstName, String lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}
```

Create a new instance with params

```java
String fullClassName = "com.zipcoder.cohort5.User";
Class aClass = Class.forName(fullClassName);

//declare the argument type for the constructor
Class[] fieldTypes = new Class[]{String.class, String.class};

//get the constructor
Constructor constructor = aClass.getDeclaredConstructor(fieldTypes);

//create the object
Object user = constructor.newInstance("Grace", "Hopper");
```
-

## The Class Object - Class name

Get the class name

```
//get class from a class
Class aclass = String.class;

//get class full name
aclass.getName(); // java.lang.String

//get the class name without the package
aclass.getSimpleName(); // String
```
-

## The Class Object - Method
`.getMethods` get all the methods

```java
public class User {
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }
}
```


```java
Class aClass = User.class;
//all public methods
Method[] methods = aClass.getMethods();

//ALL methods including private and protected
Method[] allMethods = aClass.getDeclaredMethods();
```
-


## The Class Object - Method
`.getMethod(methodName)` get a specific method

```java
public class User {
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }
}
```


```java
Class aClass = User.class;
//only public method
Method method = aClass.getMethod("getFirstName");

//for any method (public, protected, private or default)
Method amethod = aClass.getDeclaredMethod("somePrivateMethod");
```
-

## The Class Object - Method

```java
//create an instance of the user
User user = new User("Grace", "Hopper");

//get the class
Class aClass = User.class;

//declare argument type
Class[] classes = new Class[]{String.class};
//get the method with param
Method method = aClass.getMethod("setFirstName", classes);

//call the method
method.invoke(user, "Ada");
```

-
## The Class Object
- Contains info about classes
- One for every class in your program
- Once instance for every class

```java
User someUser = new User("Grace", "Hopper");
User.class == someUser.getClass(); // return true

User anotherUser = new User("Ada", "Lovelace");
anotherUser.getClass() == someUser.getClass(); //return true
```

-
## Reflection
- Use when you don't have access or know the class
- Mainly for writing library

-
### Resources

- [`Class` class documentation](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html)
- [Oracle](https://docs.oracle.com/javase/tutorial/reflect/)
- [Jenkov](http://tutorials.jenkov.com/java-reflection/index.html)
- Chapter 5.7 in Core Java volume 1
