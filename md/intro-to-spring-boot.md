# Intro to Spring Boot

-
## What is Spring?
Spring was created by Rod Johnson (2003) to simplify Java development. It is currently maintained by Pivotal.

-
## What is Spring?
- Framework
- Server side application
- Open source - source code is open and free
- Lightweight - non-invasive, low overhead

-
## What is Spring?

<img src="http://www.developersbook.com/spring/images/SpringFrameworkModules.PNG">

-
## What is Spring?
- inversion of control (IOC)
- dependency injection (DI)
- aspect oriented programming (AOP)

-
## Inversion Of Control (IOC)

- a principle in software engineering by which the control of objects or portions of a program is transferred to a container or framework
- enables a framework to take control of the flow of a program and make calls to our custom code

-
## Dependency Injection (DI)
- one way to implement IOC
- a design pattern that allows us to remove the hard-coded dependencies by setting the dependency through construction, setter, or Java reflection
- make our application loosely coupled, extendable, and maintainable

-
## Spring IoC Container

The library that constructs and injects dependencies into an object and make it ready for our use.

<img src="https://cdn.edureka.co/blog/wp-content/uploads/2017/05/ioc-1.png">

-
## Bean

An object that is instantiated, assembled, and managed by a **Spring IoC** container

-
## Aspect-Oriented Programming

- a programming approach that capture functionality that is used throughout your application into reusable components
- separate the concerns(/aspects) from the business logic
- add behavior to existing code (an advice) without modifying the code itself
- Ex: "log all function calls when the function's name begins with 'set'".

-
-
## Spring Bean
An object that is instantiated, assembled, and managed by a **Spring IoC** container

-
## Spring Bean
Annotation configuration


```java
@Component
public class Farm {
  @Autowired
  private FarmHouse farmhouse;

}
[Annotations](https://springframework.guru/spring-framework-annotations/)

```

-
## Spring Bean
XML configuration


```java
public class Person {

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

```xml
<bean id = "helloWorld" class = "com.zipcoder.spring.Person">
    <property name="name" value = "Froilan"/>
</bean>
```

-
## Spring Application Context
- IOC is represented by `ApplicationContext` interface
  - `ClassPathXmlApplicationContext`
  - `FileSystemXmlApplicationContext`
  - `AnnotationConfigApplicationContext`
- creates and wires the beans together

-
-

# Spring Boot

-
## Spring Boot
- OPINIONATED runtime for Spring projects
- Rapid Application Development

-
## Spring Boot
- sensible defaults
- auto configuration
- ability to create stand-alone and deployable applications
- full control over any configuration (xml, java config, annotions, application.properties/yml)

-
## Spring Boot

<img src="http://java9s.com/wp-content/uploads/2011/05/Spring-3-MVC-Basic-Flow.jpg">

-
### What is REST?

- REpresentational State Transfer
- architectural style for designing distributed network applications

-
### Client-Server

- Concerns should be separated between clients and servers. This enables client and server components to evolve independently and in turn allows the system to scale.

-
### Stateless

- The communication between client and server should be stateless. The server need not remember the state of the client. Instead, clients must include all of the necessary information in the request so that server can understand and process it.

-
-
## Spring Boot - Dependency
- parent
  - spring-boot-starter-parent
- spring-boot-starter-web

```XML
  <parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.2.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
			<version>1.3.5.RELEASE</version>
		</dependency>
    </dependencies>
```

-

### Annotation
- @SpringBootApplication - starting point for the application
- @Controller / @RestController
- @RequestMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping
- @PathVariable, @RequestParam, @RequestHeader, @RequestBody, @RequestAttribute, @ModelViewAttribute

-
## DEMO

-

## Resources

[Annotations](https://springframework.guru/spring-framework-annotations/)
[Spring Boot - JournalDev](https://www.journaldev.com/7969/spring-boot-tutorial)
[Spring Boot - Intro](https://spring.io/guides/gs/spring-boot/)
[Spring Boot - Rest](https://spring.io/guides/gs/rest-service/)
