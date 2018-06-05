## 6.1 Interfaces

-

# Polymorphism

What is polymorphism?

-

# Polymorphism
Polymorphism is the ability to present the same interface for different objects

-

# Polymorphism
- Interface
  - NO shared functionality/fields
- Abstract
  - SHARED SOME functionalities & fields (except private fields & methods)
- Class
  - SHARED "ALL" functionalities & fields (except private fields & methods)

-
# Polymorphism
  ```Java
    public void sort(Integer[] array) {
        // int a > int b
        //...does sorting
    }

    public void sort(Double[] array) {
        // double a > double b
        //...does sorting
    }

    public void sort(String[] array) {
        // String a > String b
        //...does sorting
    }
  ```

-
# Polymorphism

  ```Java
    public void sort(Comparable[] array) {
        // a.compareTo(b)
        // ...does sorting
    }    


    public void sortThings(){
        Integer[] intArray = {1, 4, 2, 5};
        sort(intArray);

        Double[] doubleArray = {5.1, 2.0, 4. 6};
        sort(intArray);

        String[] stringArray = {"pear", "apple", "orange"};
        sort(stringArray);
    }
  ```

-
# Polymorphism

Interface

```Java
public interface Comparable<T> {
  public int compareTo(T o);
}
```

Implementation

```Java
public class String implements Comparable<String> {
  public int compareTo(String anotherString) {
      return this.length() - anotherString.length();
  }
}

public class Integer implements Comparable<Integer> {
  public int compareTo(Integer anotherInt) {
      return (x < y) ? -1 : ((x == y) ? 0 : 1);;
  }
}
```

-
## Liskov Substitution Principle

An instance of type T can be replaced by an instance of type S if S is a subtype of T.

-
## Liskov Substitution Principle
An instance of type T can be replaced by an instance of type S if S is a subtype of T.

```Java
public void sort(Comparable[] array) {
    // a.compareTo(b)
    // ...does sorting
}
```

-
-
# Interface
An interface is not a class but a set of requirements for the classes that want to conform to the interface

-
# Interface

  * To create an interface you use the keyword `interface`
  * The interface should contain only method declarations
  * All methods of an interface are implicitly **public**

```java
public interface Comparable<T> {
  public int compareTo(T otherObj);
}
```

-
## Concrete Implementation of Interface

* The `implements` keyword is used to declare that a class is using an interface
* Within this class you _must_ implement all methods declared by the interface

```java
public class String implements Comparable<String> {
  public int compareTo(String anotherString) {
      return this.length() - anotherString.length();
  }
}

```

-
-

# Custom Comparable
* If we want our class to be sortable, we need to implement `Comparable<T>` and the `compareTo` method

```java
public class User implements Comparable<User>{
  private Integer id;
  private String name;

  public User(Integer id, String name) {
      this.id = id;
      this.name = name;
  }

  @Override
  public int compareTo(User o) {
      return this.id.compareTo(o.id);
  }
}
```

-
-
## 6.1.2 Properties of Interface

* Interfaces are not classes, you can never instantiate an interface
  * `Comparable obj = new Comparable()` (ERROR)
* You can declare a reference variable of type **interface**, as long as the class **implements** the interface

```java
Comparable intObj = 7;
Comparable doubleObj = 3.14;
Comparable strObj = "Hello!";
```

-

## A Class extends Once, implements Many.

A class can only `extends` a single class, but it can `implements` many interfaces

```java
public abstract User {
  String getName();
}

public abstract Admin {
  boolean hasAccess(String request);
}
```

This code will not compile:


```java
public class Manager extends User, Admin {
  // Error
}
```
-
A class can implements many

```java
public interface User {
    String getName();
}

public interface Admin {
  boolean hasAccess(String request);
}
```

This works!
```java
public class Manager implements User, Admin{

}

```

-
-

##Static Methods

In Java 8+, static method are allowed in an interface

```java
public interface User {
    public static User[] getAllUsers(){
        return Database.getAllUsers();
    }
}
```
-
-
##Default Methods

* In Java 8+, you can have a default method for an interface.
* Add the keyword `default` to the method
* Classes that want to override the method will create the same method and tag it with the **@Override** annotation

-

```java
public interface User {

  /**
   * By default the user doesn't have any role
   **/
  default Role[] getRoles(){
    return new Role[0];
  }
}
```
-
# Overriding default

```java
public class Student {

  @Override
  public Role[] getRoles(){
    return new Role[]{Role.STUDENT};
  }
}
```
-
-
## 6.1.6 Resolving Default Method Conflicts

When implementing two interfaces with the same default methods, you have to override the method.

```java
public interface Admin {
    default String getName(){
        return "";
    }
}

public interface User {
    default String getName() {
        return "Test User";
    }
}
```
-
Overriding default method with our implementation

```java
public class Staff implements User, Admin{
    private String name;
    /**
     * Here we have a class that implements two interfaces with
     * default implementations the compiler has no way of implicitly
     * knowing who should be called so we have to explicitly state it
     **/
    @Override
    public String getName() {
        return name;
    }
}
```
-
Overriding default method with interface default method

```java
public class Staff implements User, Admin{
    /**
     * You still have to implement it because Java doesn't
     * know how to resolve the conflict
     **/
    @Override
    public String getName() {
        return Admin.super.getName();
    }
}
```

-
## Interface vs Abstract
-

# Polymorphism
- Interface
  - NO shared functionality/fields
- Abstract
  - SHARED SOME functionalities & fields (except private fields & methods)
- Class
  - SHARED "ALL" functionalities & fields (except private fields & methods)

-
-

<img src = 'https://c-7npsfqifvt34x24jnhjyx2esbolfsx2edpn.g00.ranker.com/g00/3_c-7x78x78x78.sbolfs.dpn_/c-7NPSFQIFVT34x24iuuqtx3ax2fx2fjnhjy.sbolfs.dpnx2fvtfs_opef_jnhx2f61117x2f2111210247x2fpsjhjobmx2fnjoj-qjht-qipup-v2x3fx78x3d761x26rx3d61x26gnx3dkqhx26gjux3ddspqx26dspqx3dgbdftx26j21d.nbslx3djnbhf_$/$/$/$/$/$'>

-
-

## Interfaces and Callbacks

A callback method in Java is a method that gets called when an event occurs. Usually, you can implement that by passing an implementation of a certain interface to the system that is responsible for triggering the event E.

-
```java
public interface java.awt.event.ActionListener {
  void actionPerformed(ActionEvent e);
}
```

```java
public class ScanForNinjas implements ActionListener {

    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("All clear no ninjas at " + e.getWhen() + " time");
    }
}
```

-

Scan for Ninjas every second.
```
public class ScanForEnemies {

    public static void main(String [] args){
        ActionListener scanForNinjas = new ScanForNinjas();

        // Creates a Timer and initializes both the initial delay and between-event delay to delay milliseconds.
        // scanForNinjas gets a call to actionPerformed method every 1000 msecs.
        Timer t = new Timer(1000, scanForNinjas);
        t.start();
        JOptionPane.showMessageDialog(null, "Quit program?");

       System.exit(0);
    }
}
```
-
-
##Lambda Expressions

* lambda expression - is a block of code that you can pass around so it can be executed later, once or multiple times.
* functional programming - a style of building the structure and elements of computer programs—that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data.

-

## Interface `Comparator<T>`

* Type Parameters:`T` - the type of objects that may be compared by this comparator
* Functional Interface: has only one abstract method. Therefore it created with a lambda expression or method reference
-
```java
public class SpeedComparator implements Comparator<Person> {

   public int compare(Person one, Person two){
     return one.speed() - two.speed();
   }
}
```

```java
Arrays.sort(people, new SpeedComparator());
```

-
* There is no reason to create a class just to implement a Comparator
* We can create a Lambda Expression instead

-

```java
public class Person {

    public int speed;

    public Person(int speed){
        this.speed = speed;    
    }
}
```

-
```java
public class Race {

  public void runRace(){
    Person slowPerson = new Person(1);
    Person fastPerson = new Person(100);

    Person[] people = new Person[]{ slowPerson, fastPerson};

    // We can create a reference using the interface Comparator
    // Then create the implementation needed for the single method

    Comparator<Person> speedComparator = (racerOne, racerTwo) -> racerOne.speed - racerTwo.speed;

    Arrays.sort(people, speedComparator);
  }

}
```
-
-

<img src = 'https://i0.wp.com/theverybesttop10.com/wp-content/uploads/2014/06/Top-10-Baby-Chicks-in-Hats-1.jpg?resize=510%2C410&ssl=1'>
