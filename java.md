## Core Java Concepts

### 1. What is Java?
Java is a popular programming language that is platform-independent (write once, run anywhere). It is used for web, mobile, desktop, and enterprise applications.

```bash 
java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); 
    }
}
(Output: Hello, World!)
```

### 2. What are the features of Java?
- Simple (Easy to learn)

- Object-Oriented (Uses classes & objects)

- Platform-independent (Runs on any OS with JVM)

- Secure (No pointers, bytecode verification)

- Multithreaded (Supports concurrent execution)

### 3. What is the difference between JDK, JRE, and JVM
- **JVM (Java Virtual Machine):** An abstract machine that provides runtime environment to execute Java bytecode.

- **JRE (Java Runtime Environment):** Implementation of JVM + libraries needed to run Java applications.

- **JDK (Java Development Kit):** JRE + development tools (compiler, debugger, etc.) needed to develop Java applications.

Example:

- When you write code (.java file), JDK's javac compiles it to .class (bytecode)

- JRE provides libraries to run this .class file

- JVM executes the bytecode on any platform

### 4. Explain public static void main(String args[])
This is the entry point for any Java application.

- public: Accessible from anywhere

- static: Can be called without creating an instance of the class

- void: Doesn't return anything

- main: Method name recognized by JVM

- String args[]: Command line arguments

Example:
```bash
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        for(String arg : args) {
            System.out.println("Argument: " + arg);
        }
    }
}
```
### 5. What are Java's primitive data types?

Java has 8 primitive data types:

- byte (8-bit signed integer)

- short (16-bit signed integer)

- int (32-bit signed integer)

- long (64-bit signed integer)

- float (32-bit floating point)

- double (64-bit floating point)

- char (16-bit Unicode character)

- boolean (true/false)

Example:
```bash 
byte b = 100;
short s = 10000;
int i = 100000;
long l = 10000000000L; // Note the 'L' suffix
float f = 3.14f;       // Note the 'f' suffix
double d = 3.1415926535;
char c = 'A';
boolean bool = true;
```

### 6. What are variables in Java?
Variables store data.

Types:

- Local variable (Inside a method)

- Instance variable (Inside a class, outside methods)

- Static variable (Shared among all objects)

```bash 
class Test {
    int instanceVar = 10; // Instance variable
    static int staticVar = 20; // Static variable

    void method() {
        int localVar = 30; // Local variable
    }
}
```

### 7. What is a constructor?
A special method that initializes objects.
```bash
java
class Car {
    String name;
    
    // Constructor
    Car(String n) {
        name = n;
    }
}

Car myCar = new Car("Toyota"); // Constructor called
```

### 8. What is a static keyword?
Belongs to the class, not the object.

```bash
java
class Counter {
    static int count = 0; // Shared among all objects
    
    Counter() { count++; }
}

Counter c1 = new Counter(); // count = 1  
Counter c2 = new Counter(); // count = 2  
```
### 9. What is the final keyword?
Makes a variable constant, a method non-overridable, or a class non-inheritable.

```bash
java
final int AGE = 25; // Constant  
AGE = 30; // Error (cannot change)
```
### 10. What is a package in Java?
A folder that groups related classes.
```bash
java
package com.mycompany;  
import java.util.Scanner;  
```
### 11. What is a String in Java?
A sequence of characters ("Hello").
```bash
java
String name = "Java";  
System.out.println(name.length()); // 4  
```
### 12. Why is String immutable?
Once created, it cannot be changed (for security & thread safety).
```bash
java
String s = "Hello";  
s.concat(" World"); // Doesn't modify 's'  
System.out.println(s); // "Hello"  
```

### 13. What is StringBuffer and StringBuilder?
- StringBuffer → Thread-safe (slower).

- StringBuilder → Not thread-safe (faster).
```bash
java
StringBuilder sb = new StringBuilder("Hello");  
sb.append(" World");  
System.out.println(sb); // "Hello World"
```

### 14. What are generics in Java?
Allows type-safe collections.
```bash
java
List<String> list = new ArrayList<>();  
list.add("Hello");  
// list.add(10); → Error (type safety)
```
### 15. What is autoboxing and unboxing?
Autoboxing → int → Integer

Unboxing → Integer → int
```bash
java
Integer num = 10; // Autoboxing  
int n = num;      // Unboxing  
```

### 16. What are annotations in Java?
Metadata for code (@Override, @Deprecated).
```bash
java
@Override  
void myMethod() { }  
```

### 17. What is the difference between final, finally, and finalize?
- final → Constant variable/method/class.

- finally → Block that always executes in try-catch.

- finalize() → Method called before garbage collection.

### 18. What is the super keyword?
Refers to the parent class.
```bash
java
class Parent {  
    void show() { System.out.println("Parent"); }  
}  

class Child extends Parent {  
    void show() {  
        super.show(); // Calls Parent's show()  
    }  
}  
```
### 19. What is the this keyword?
Refers to the current object.
```bash
java
class Student {  
    String name;  
    Student(String name) {  
        this.name = name; // Refers to current object  
    }  
}  
```
### 20. What is a Java bean?
A class with:

- Private fields

- Public getters/setters

- No-arg constructor
```bash
java
class User {  
    private String name;  
    public String getName() { return name; }  
    public void setName(String n) { name = n; }  
}  
```
### 21. What is the difference between break and continue?
- break → Exits the loop.

- continue → Skips current iteration.
```bash
java
for (int i = 1; i <= 5; i++) {  
    if (i == 3) break;    // Exits at 3  
    if (i == 2) continue; // Skips 2  
    System.out.println(i);  
}  
// Output: 1  
```



## Object-Oriented Programming

### 1. Explain the four pillars of OOP in Java
- **Encapsulation:** Binding data and methods together, hiding internal details
```bash
public class Person {
    private String name; // private = encapsulated
    
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```
- **Inheritance:** Creating new classes from existing ones

```bash
class Animal { void eat() { System.out.println("eating"); } }
class Dog extends Animal { void bark() { System.out.println("barking"); } }
```

- **Polymorphism:** One interface, multiple implementations

```bash
interface Shape { void draw(); }
class Circle implements Shape { public void draw() { /* draw circle */ } }
class Square implements Shape { public void draw() { /* draw square */ } }
```
- **Abstraction:** Hiding complex implementation details

```bash
abstract class Vehicle {
    abstract void run(); // abstract method
    void stop() { System.out.println("Vehicle stopped"); } // concrete method
}
```

### 2. Difference between abstract class and interface

| Feature            | Abstract Class                      | Interface                              |
|--------------------|-------------------------------------|----------------------------------------|
| **Methods**        | Can have abstract and concrete      | All abstract (before Java 8)           |
| **Variables**      | Can have any type of variables      | Only public static final               |
| **Inheritance**    | Single inheritance                  | Multiple inheritance possible          |
| **Default methods**| Not applicable                      | Supported (Java 8+)                    |
| **Constructor**    | Can have constructor                | No constructor                         |
| **Access modifiers**| Can have any access modifier       | Public by default                      |


```bash
java
// Abstract class
abstract class Animal {
    abstract void makeSound();
    void eat() { System.out.println("Eating..."); }
}

// Interface
interface Drivable {
    void drive(); // abstract method
    default void honk() { System.out.println("Honking!"); } // default method (Java 8+)
}

class Car implements Drivable {
    public void drive() { System.out.println("Driving car"); }
}
```

### 3. What is method overloading?
Multiple methods with the same name but different parameters.
```bash
java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```

### 4. What is method overriding?
When a child class provides its own implementation of a method from the parent class.

```bash
java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}

class Dog extends Animal {
    @Override
    void sound() { System.out.println("Bark!"); }
}
```

## Exception Handling
### 1. Explain Java's exception hierarchy

```bash
Throwable
├── Error (e.g., OutOfMemoryError, StackOverflowError)
└── Exception
    ├── RuntimeException (unchecked, e.g., NullPointerException)
    └── Checked Exceptions (e.g., IOException)
```

```bash 
java
try {
    FileReader file = new FileReader("nonexistent.txt");
} catch (FileNotFoundException e) { // Checked exception
    System.out.println("File not found: " + e.getMessage());
} catch (Exception e) { // General exception
    System.out.println("Something went wrong");
} finally {
    System.out.println("This always executes");
}
```

## Collections Framework

### 1. Explain Java Collections Framework hierarchy
```bash
Iterable
└── Collection
    ├── List (ArrayList, LinkedList, Vector)
    ├── Set (HashSet, LinkedHashSet, TreeSet)
    └── Queue (PriorityQueue, Deque)
Map (HashMap, LinkedHashMap, TreeMap, Hashtable)
```

Example:
```bash
java
// List example
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
System.out.println(list.get(0)); // Apple

// Set example
Set<Integer> set = new HashSet<>();
set.add(1); set.add(1); set.add(2);
System.out.println(set); // [1, 2]

// Map example
Map<String, Integer> map = new HashMap<>();
map.put("John", 25);
map.put("Jane", 30);
System.out.println(map.get("John")); // 25
```


### 2. Difference between ArrayList and LinkedList

| Feature        | ArrayList                           | LinkedList                             |
|----------------|--------------------------------------|-----------------------------------------|
| **Underlying** | Dynamic array                        | Doubly linked list                      |
| **Access**     | Fast O(1) random access              | Slow O(n) random access                 |
| **Insert/Delete** | Slow O(n) (needs shifting)       | Fast O(1) at beginning/end              |
| **Memory**     | Less overhead (only data)            | More overhead (links + data)           |
| **Use cases**  | Frequent access, less modification   | Frequent modification                  |

Example:

```bash
java
List<String> arrayList = new ArrayList<>();
arrayList.add("A"); // O(1) if no resize needed
arrayList.get(0);   // O(1)

List<String> linkedList = new LinkedList<>();
linkedList.add("B"); // O(1)
linkedList.get(0);   // O(n)
```

## Multithreading

### 1. What is a thread in Java?
A thread is a lightweight sub-process that runs within a program. It's like having multiple workers in a factory - while one worker is assembling a product, another can be packaging it, making the whole process faster.

Example:
```bash
java
public class SimpleThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
    
    public static void main(String args[]) {
        SimpleThread t1 = new SimpleThread();
        t1.start(); // starts the thread
    }
}
```

### 2. How to create a thread in Java?

Two ways to create threads:

- Extending Thread class

- Implementing Runnable interface

Example:
```bash
java
// Method 1: Extending Thread
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}

// Method 2: Implementing Runnable
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable is running");
    }
}

public class Main {
    public static void main(String[] args) {
        // Method 1
        MyThread t1 = new MyThread();
        t1.start();
        
        // Method 2
        Thread t2 = new Thread(new MyRunnable());
        t2.start();
        
        // Lambda expression (Java 8+)
        Thread t3 = new Thread(() -> System.out.println("Lambda thread"));
        t3.start();
    }
}
```

### 3. What is synchronization in Java?
Synchronization is the capability to control access to shared resources by multiple threads to prevent race conditions.

Example:

```bash
java
class Counter {
    private int count = 0;
    
    // Synchronized method
    public synchronized void increment() {
        count++;
    }
    
    // Synchronized block
    public void decrement() {
        synchronized(this) {
            count--;
        }
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });
        
        t1.start(); t2.start();
        t1.join(); t2.join();
        
        System.out.println("Final count: " + counter.getCount()); // Should be 2000
    }
}
```

### 4. What are the states of a thread in Java?
A thread can be in one of these states:

- New: Just created but not started yet

- Runnable: Ready to run or currently running

- Blocked/Waiting: Waiting for a resource or another thread

- Timed Waiting: Waiting for a specific time period

- Terminated: Completed execution

It's like a person's daily routine:

- New: Just woke up

- Runnable: Getting ready for work

- Blocked: Waiting for the bus

- Timed Waiting: Taking a scheduled lunch break

- Terminated: Going to sleep

### 10. What is the difference between synchronized methods and synchronized blocks?
- **Synchronized method:** Locks the entire object. Like locking the entire office when one person is working.

- **Synchronized block:** Locks only a specific part. Like locking just the meeting room when it's in use.

Example:
```bash
java
class Example {
    // Synchronized method
    public synchronized void method1() {
        // Entire method is synchronized
    }
    
    // Synchronized block
    public void method2() {
        // Non-critical code here
        
        synchronized(this) {
            // Only this block is synchronized
        }
        
        // More non-critical code here
    }
}
```

### 11. What is a race condition and how can you prevent it?
Answer:
A race condition is like two people trying to withdraw money from the same bank account at the same time, causing incorrect balance. It happens when multiple threads access shared data and try to change it simultaneously.

Example (race condition):
```bash
java
class BankAccount {
    private int balance = 100;
    
    public void withdraw(int amount) {
        if (balance >= amount) {
            balance -= amount;
        }
    }
    
    public int getBalance() {
        return balance;
    }
}
```
Solution (using synchronization):
```bash
java
class BankAccount {
    private int balance = 100;
    
    public synchronized void withdraw(int amount) {
        if (balance >= amount) {
            balance -= amount;
        }
    }
    
    public int getBalance() {
        return balance;
    }
}
```

## Java 8 Features
### 1. Explain Lambda expressions and Functional Interfaces
- Lambda expressions: Anonymous functions that can be passed around

- Functional interfaces: Interfaces with exactly one abstract method (@FunctionalInterface)

```bash
Example:

java
// Functional interface
@FunctionalInterface
interface Greeting {
    void sayHello(String name);
}

public class Main {
    public static void main(String[] args) {
        // Lambda expression implementation
        Greeting greet = (name) -> System.out.println("Hello, " + name);
        greet.sayHello("John");
        
        // Built-in functional interfaces
        Consumer<String> consumer = s -> System.out.println(s.toUpperCase());
        consumer.accept("hello");
        
        Function<Integer, String> function = i -> "Number: " + i;
        System.out.println(function.apply(5));
        
        Predicate<Integer> predicate = i -> i > 10;
        System.out.println(predicate.test(15)); // true
    }
}
```

### 2. What are Streams in Java 8?
Streams represent a sequence of elements supporting sequential and parallel aggregate operations.

Example:
```bash
java
List<String> names = Arrays.asList("John", "Alice", "Bob", "Anna");

// Filter names starting with 'A' and convert to uppercase
List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());

System.out.println(result); // [ALICE, ANNA]

// Parallel stream example
long count = names.parallelStream()
    .filter(name -> name.length() > 3)
    .count();
```

## Advanced Java Questions
### 1. Explain Java Memory Model
Java Memory Model divides memory into:

1. **Heap:** Stores objects (shared across threads)

- Young Generation (Eden, S0, S1)

- Old Generation

2. **Stack:** Stores method calls and local variables (per thread)

3. **Method Area:** Stores class structures, static variables

4. **PC Registers:** Stores thread execution address

5. **Native Method Stack:** For native methods

Example:
```bash
java
public class MemoryExample {
    static int staticVar = 1; // Method Area
    int instanceVar = 2;     // Heap
    
    public static void main(String[] args) {
        int localVar = 3;    // Stack
        MemoryExample obj = new MemoryExample(); // obj reference in stack, object in heap
    }
}
```

### 2. What is the difference between == and equals()?

- == compares references (memory addresses)

- equals() compares content (can be overridden)

```bash
java
String s1 = new String("Hello");
String s2 = new String("Hello");
String s3 = s1;

System.out.println(s1 == s2);      // false (different references)
System.out.println(s1 == s3);      // true (same reference)
System.out.println(s1.equals(s2)); // true (same content)

// For custom objects, need to override equals()
class Person {
    String name;
    Person(String name) { this.name = name; }
    
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person p = (Person) o;
        return name.equals(p.name);
    }
}
```

### 3. What are Java Annotations?
Annotations provide metadata about the code that can be used by the compiler or at runtime.

#### Built-in annotations:

- @Override, @Deprecated, @SuppressWarnings

- @FunctionalInterface (Java 8)

- @SafeVarargs (Java 7)

Example:
```bash
java
// Custom annotation
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface MyAnnotation {
    String value() default "default";
    int count() default 1;
}

// Using annotation
class AnnotationExample {
    @MyAnnotation(value = "test", count = 3)
    public void myMethod() { /* ... */ }
    
    @Override
    public String toString() { return "Overridden toString"; }
    
    @Deprecated
    public void oldMethod() { /* ... */ }
}
```

## JDBC Questions
#### 1. Explain JDBC workflow

- Load the JDBC driver

- Establish connection

- Create statement

- Execute query

- Process results

- Close connection

```bash
public class JdbcExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydb";
        String user = "root";
        String password = "password";
        
        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT * FROM employees")) {
            
            while (rs.next()) {
                System.out.println(rs.getInt("id") + " " + rs.getString("name"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## Design Patterns

### 1. Explain Singleton pattern in Java
Ensures a class has only one instance and provides a global point of access to it.

Implementation approaches:

- Eager initialization

- Lazy initialization

- Thread-safe initialization

- Bill Pugh Singleton (using static inner class)

- Enum Singleton (most recommended)

Example (Bill Pugh Singleton):

```bash
java
public class Singleton {
    private Singleton() {} // private constructor
    
    private static class SingletonHelper {
        private static final Singleton INSTANCE = new Singleton();
    }
    
    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
    
    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}

// Usage:
Singleton singleton = Singleton.getInstance();
singleton.showMessage();
```

### 2. Explain the Factory Design Pattern
The Factory pattern provides an interface for creating objects while allowing subclasses to alter the type of objects created.

When to use:

When object creation logic is complex

When you need to decouple object creation from usage

When you want to provide different implementations

Example:
```bash
java
interface Shape {
    void draw();
}

class Circle implements Shape {
    public void draw() { System.out.println("Drawing Circle"); }
}

class Square implements Shape {
    public void draw() { System.out.println("Drawing Square"); }
}

class ShapeFactory {
    public Shape getShape(String shapeType) {
        if (shapeType == null) return null;
        if (shapeType.equalsIgnoreCase("CIRCLE")) return new Circle();
        if (shapeType.equalsIgnoreCase("SQUARE")) return new Square();
        return null;
    }
}


// Usage:
ShapeFactory factory = new ShapeFactory();
Shape shape = factory.getShape("CIRCLE");
shape.draw(); // Drawing Circle
```
### 25. What is the Observer Pattern?
The Observer pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.

- Java implementations:

- java.util.Observable (deprecated in Java 9)

- PropertyChangeListener in Swing

- Modern approach using custom implementation

Example:
```bash
java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

interface Subject {
    void register(Observer o);
    void unregister(Observer o);
    void notifyObservers();
}

class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String news;
    
    public void setNews(String news) {
        this.news = news;
        notifyObservers();
    }
    
    public void register(Observer o) { observers.add(o); }
    public void unregister(Observer o) { observers.remove(o); }
    public void notifyObservers() {
        for (Observer o : observers) {
            o.update(news);
        }
    }
}

class NewsChannel implements Observer {
    private String news;
    
    public void update(String news) {
        this.news = news;
        display();
    }
    
    public void display() {
        System.out.println("Breaking News: " + news);
    }
}

// Usage:
NewsAgency agency = new NewsAgency();
NewsChannel channel1 = new NewsChannel();
NewsChannel channel2 = new NewsChannel();

agency.register(channel1);
agency.register(channel2);
agency.setNews("Java 17 released!"); // Both channels display the news
```

## Java Best Practices

### 1. What are immutable objects and how to create them?
Answer:
Immutable objects cannot be modified after creation. Benefits include thread-safety and simplicity.

Rules to create immutable objects:

- Make class final

- Make all fields final and private

- Don't provide setter methods

- Make defensive copies of mutable objects

- Don't allow subclasses to override methods

```bash 
java
public final class ImmutablePerson {
    private final String name;
    private final int age;
    private final List<String> hobbies;
    
    public ImmutablePerson(String name, int age, List<String> hobbies) {
        this.name = name;
        this.age = age;
        this.hobbies = Collections.unmodifiableList(new ArrayList<>(hobbies)); // defensive copy
    }
    
    public String getName() { return name; }
    public int getAge() { return age; }
    public List<String> getHobbies() { return hobbies; } // returns unmodifiable list
}
```

## Java 11+ Features
### 1. What are some new features in Java 11?

- Local Variable Type Inference (var keyword)

- New String methods (isBlank(), lines(), repeat(), strip())

- New File methods (readString(), writeString())

- HTTP Client API (standardized)

- Launch Single-File Source-Code Programs

Example:
```bash
java
// var keyword
var list = new ArrayList<String>(); // inferred as ArrayList<String>

// New String methods
String multiline = "Hello\nWorld\nJava";
multiline.lines().forEach(System.out::println);

// Files.readString
String content = Files.readString(Path.of("file.txt"));

// HTTP Client
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://example.com"))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

## Performance Tuning
### 1. How to improve Java application performance?

- Use StringBuilder for string concatenation in loops

- Avoid unnecessary object creation

- Use primitive types instead of wrappers when possible

- Initialize collections with proper capacity

- Use enhanced for loops where possible

- Consider using concurrent collections for multithreaded access

- Use profiling tools (VisualVM, JProfiler)

- Tune JVM parameters (-Xms, -Xmx, GC settings)

Example:
```bash
java
// Bad - creates multiple String objects
String result = "";
for (int i = 0; i < 100; i++) {
    result += i; // creates new String each time
}

// Good - uses StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 100; i++) {
    sb.append(i);
}
String result = sb.toString();

// Initialize ArrayList with capacity if size is known
List<String> list = new ArrayList<>(1000); // avoids resizing
```

## Core Java 8 Features
### 1. What are the main features introduced in Java 8?
Answer:
Java 8 introduced several major features that changed how we write Java code:

- Lambda Expressions - Enable functional programming

- Stream API - For bulk data operations on collections

- Functional Interfaces - Single abstract method interfaces

- Default Methods - Methods with implementation in interfaces

- Method References - Shorthand for lambdas calling existing methods

- Optional Class - To handle null values better

- New Date/Time API - Improved date/time handling (java.time package)

- Nashorn JavaScript Engine - New JavaScript engine

### Lambda Expressions
### 2. What are lambda expressions in Java 8?
Lambda expressions are like shortcuts to write small anonymous functions (methods without names). They make your code cleaner when working with interfaces that have just one method.

Syntax:
```bash
java
(parameters) -> { body }
Example:

java
// Old way (anonymous class)
Runnable r1 = new Runnable() {
    public void run() {
        System.out.println("Running without lambda");
    }
};

// New way (lambda)
Runnable r2 = () -> System.out.println("Running with lambda");
```
### 3. What are functional interfaces?
A functional interface is an interface with exactly one abstract method (but can have many default methods). They're the basis for lambda expressions.

Example:
```bash
java
@FunctionalInterface
interface Greeting {
    void sayHello(String name); // single abstract method
    
    default void defaultMethod() { // default method is OK
        System.out.println("Default method");
    }
}

public class Main {
    public static void main(String[] args) {
        Greeting greet = (name) -> System.out.println("Hello " + name);
        greet.sayHello("Alice"); // Output: Hello Alice
    }
}
```
### Stream API
### 4. What is the Stream API in Java 8?
The Stream API is like a conveyor belt for processing collections of objects. It allows you to perform operations like filtering, mapping, and reducing on collections in a declarative way.

Key Features:

- Doesn't store data itself

- Doesn't modify the original collection

- Operations are lazy (only execute when needed)

Example:
```bash
java
List<String> names = Arrays.asList("John", "Alice", "Bob", "Charlie");

// Filter names starting with 'A' and convert to uppercase
List<String> result = names.stream()
                          .filter(name -> name.startsWith("A"))
                          .map(String::toUpperCase)
                          .collect(Collectors.toList());
// result = ["ALICE"]
```
### 5. What's the difference between intermediate and terminal operations in Streams?
Answer:

Intermediate operations:

Return a new stream (lazy evaluation)

Examples: filter(), map(), sorted(), distinct()

Terminal operations:

Produce a result or side-effect

End the stream pipeline

Examples: forEach(), collect(), count(), reduce()

Example:
```bash
java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Intermediate operations (filter and map)
// Terminal operation (forEach)
numbers.stream()
       .filter(n -> n % 2 == 0)  // intermediate
       .map(n -> n * 2)          // intermediate
       .forEach(System.out::println); // terminal
```       
### Default and Static Methods
### 6. What are default methods in interfaces?
Default methods let you add new methods to interfaces without breaking existing implementations. They have a default implementation.

Example:
```bash
java
interface Vehicle {
    void start(); // traditional abstract method
    
    default void honk() { // default method
        System.out.println("Beep beep!");
    }
}

class Car implements Vehicle {
    public void start() {
        System.out.println("Car started");
    }
    // honk() is inherited automatically
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.start(); // Car started
        car.honk();   // Beep beep!
    }
}
```

### 7. Can interfaces have static methods in Java 8?
Yes! Java 8 allows static methods in interfaces, which are useful for utility methods.

Example:
```bash
java
interface MathOperations {
    static int add(int a, int b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        int sum = MathOperations.add(5, 3); // Calling static method
        System.out.println(sum); // 8
    }
}
```
### Optional Class
### 8. What is the Optional class in Java 8?
Optional is like a box that might contain a value or might be empty (instead of using null). It helps avoid NullPointerExceptions.

Common Methods:

- of() - Creates Optional with non-null value

- empty() - Creates empty Optional

- ofNullable() - Creates Optional that may be empty

- isPresent() - Checks if value exists

- get() - Gets the value (throws exception if empty)

- orElse() - Provides default value if empty

Example:
```bash
java
Optional<String> name = Optional.ofNullable(getNameFromDatabase());
String result = name.orElse("Default Name");

// Safe operations
name.ifPresent(n -> System.out.println("Name is: " + n));
```
### Date/Time API
### 9. What's wrong with the old Date/Calendar classes and what's new in Java 8?
Answer:
Problems with old API:

- Not thread-safe

- Poor design (months 0-based, years starting from 1900)

- Difficult to use

- New java.time package (JSR-310) features:

- LocalDate - date without time

- LocalTime - time without date

- LocalDateTime - date and time

- ZonedDateTime - date/time with timezone

- Period - difference between dates

- Duration - difference between times

Example:
```bash
java
// Old way
Date oldDate = new Date(); // mutable and not thread-safe

// New way
LocalDate today = LocalDate.now();
LocalDate birthday = LocalDate.of(1990, Month.JANUARY, 1);
Period age = Period.between(birthday, today);

System.out.println("You are " + age.getYears() + " years old");
Method References
```
### 10. What are method references in Java 8?
Answer:
Method references are shorthand notation for lambda expressions that just call an existing method. They make code more readable.

Types:

- Class::staticMethod - Reference to static method

- object::instanceMethod - Reference to instance method of particular object

- Class::instanceMethod - Reference to instance method of arbitrary object

- Class::new - Constructor reference

Examples:
```bash
java
// Lambda
names.forEach(name -> System.out.println(name));

// Method reference
names.forEach(System.out::println);

// Static method reference
List<Integer> numbers = Arrays.asList(1, 2, 3);
numbers.stream()
       .map(String::valueOf) // same as n -> String.valueOf(n)
       .forEach(System.out::println);
```
### Parallel Streams
### 11. What are parallel streams in Java 8?
Answer:
Parallel streams split the work across multiple threads automatically to leverage multi-core processors. Just add parallel() to a stream pipeline.

Example:
```bash
java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Sequential stream
numbers.stream().filter(n -> n % 2 == 0).forEach(System.out::println);

// Parallel stream
numbers.parallelStream().filter(n -> n % 2 == 0).forEach(System.out::println);
```
Note: Use parallel streams carefully - they have overhead and aren't always faster, especially for small datasets or I/O-bound operations.
