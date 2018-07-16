#Intro to design patterns
-
-
## What is design patterns?
  <p class="fragment fade-up">Design pattern is a general, reusable solution to a common problem in software design</p>

-
## Why use design patterns?
- Communication
  - Establish vocabulary which communicates a problem, solution, and potential consequences
- Maintainability
- Loose Coupling

-
## OO Principles
- Encapsulates what varies
- Favor composition over Inheritance
- Program to interfaces, not implementations
- Strives for loosely coupled designs
- Classes should be open for open for extensions but closed for modification

-
## What design patterns are not
- Copy and paste solutions
- Showing off your knowledge

-
-
# Four Essential Elements of a Pattern
1. Pattern Name
2. Problem
3. Solution
4. Consequences

-
# 1. Pattern name
* a word or two we can use to describe a design
	* problem
	* solution
	* consequence

* Naming increases design vocabulary
* Enables discussion and design at a higher level of abstraction.
* "Bisected Oval Pattern"

-
# 2. Problem
* Describes when to apply pattern
* Explains problem and its context
* Sometimes problems will include a list of conditions that must be met before it makes sense to apply the pattern.
* "Is our subject facing forward?"

-
# 3. Solution
* Describes the elements that make up the design, their relationships, respobsibilities, and collaborations.
* Provides an abstract description of a design problem and how a general arrangement of elements solves it.
* "_Oval bisection_ allows early planning for placement of facial features"

-
# 4. Consequences
* The results and trade-offs of applying the pattern.
* Address memory, time, and language implementation issues.
* Include impact on a system's flexibilitiy, extensibility, portability.
* "Yields a forward facing portrait. Does not support profile portraits."


-
## Types of design patterns
- **Structural** - forms larger structures from individual parts (e.g. decorator)
- **Creational** - encapsulates the constructions of the objects (e.g. factory)
- **Behavioral** - defines interactions between objects and focus on how objects communicate with each other (e.g. command)

-
-
## Structural patterns
- Decorator
- Facade
- Adapter
- Proxy
- Bridge
- Composite

-
## Decorator pattern
- **Problem**: add functionalities to an existing object dynamically, without extend it

[Wiki decorator pattern](https://en.wikipedia.org/wiki/Decorator_pattern)
-
## Decorator pattern

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Decorator_UML_class_diagram.svg/960px-Decorator_UML_class_diagram.svg.png" width=650px>

-
## Decorator pattern

<img src="https://shishirkumarblog.files.wordpress.com/2011/07/decorator_pattern.jpg" width=500px>

Decorator: BufferedInputStream, CheckedInputStream, CipherInputStream, DataInputStream,  DigestInputStream

-
## Facade Pattern
**Problem**: simplify the usage of a complex code

[Wiki Facade pattern](https://en.wikipedia.org/wiki/Facade_pattern)
-
## Facade pattern

<img src="http://gyanendushekhar.com/wp-content/uploads/2016/08/Facade-Design-Pattern-in-C-UML-Diagram.png" width=650px>

-
## Facade pattern
Think of building a queue, using a List
Queue only has two methods
- push
- pop

-
## Adapter pattern
**Problem**: client requires a different interface

-
## Adapter pattern

<img src="https://upload.wikimedia.org/wikipedia/commons/e/e5/W3sDesign_Adapter_Design_Pattern_UML.jpg" width=650px>

-
## Proxy pattern
**Problem**: add additional functionality when accessing an object

-
## Proxy pattern

<img src="https://upload.wikimedia.org/wikipedia/commons/7/75/Proxy_pattern_diagram.svg">

-
## Composite pattern
**Problem**: needs to treat a part and a whole object as one

-
## Composite pattern

<img src="https://upload.wikimedia.org/wikipedia/commons/5/5a/Composite_UML_class_diagram_%28fixed%29.svg" width=650px>
-

<img src="http://4.bp.blogspot.com/-iGG4tneZf5c/T5wMXUQ0fYI/AAAAAAAADAQ/JkxcggowDgE/s1600/Cute-Kittens-kittens-16123995-1280-800.jpg">

-
-
## Creational patterns
Encapsulates the constructions of the objects
- Abstract Factory
- Builder
- Factory Method
- Prototype
- Singleton
