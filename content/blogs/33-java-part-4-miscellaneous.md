---
title: "Java Crash Course - Part 4 (Miscellaneous)"
description: "Let's learn writing program with Java"
date: 2025-09-29
tags: ["programming", "language", "java", "crash-course", "miscellaneous"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/30-java-language.webp"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 3:** [Java Crash Course - Part 3 (Object Oriented Programming)]({{< ref "blogs/32-java-part-3-oop.md" >}})
---

{{< figure
    src="/img/blogs/30-java-language.webp"
    caption="Java Programming Language (Photo Credit: Orient Software)"
    align=center
>}}

Let's explore some more features or language building blocks that Java support.

### Enum:
An enum is a special type of class in Java that represents a group of constants. Enums are used to create fixed sets of constants that are used in a program. They make code more readable and less error-prone because they provide a set of named values that can be used instead of hard-coded values.

Example:
```java
public enum Direction {
  NORTH,
  EAST,
  SOUTH,
  WEST
}


//Using an enum in a switch statement:
Direction direction = Direction.NORTH;
switch(direction) {
  case NORTH:
    System.out.println("Going North");
    break;
  case EAST:
    System.out.println("Going East");
    break;
  case SOUTH:
    System.out.println("Going South");
    break;
  case WEST:
    System.out.println("Going West");
    break;
}
```

In Java one of the advantages of enums is that you can define custom values for each constant. 

Here's an example of how to do that:
```java
public enum Size {
    SMALL("S"), MEDIUM("M"), LARGE("L"), XLARGE("XL");
    
    private final String abbreviation;
    
    private Size(String abbreviation) {
        this.abbreviation = abbreviation;
    }
    
    public String getAbbreviation() {
        return abbreviation;
    }
}

Size size = Size.MEDIUM;
System.out.println("Size: " + size);
System.out.println("Abbreviation: " + size.getAbbreviation());
```

### Annotation:
Annotations are a way to add metadata to Java code. They can be added to classes, methods, variables, and parameters. Annotations are used for a variety of purposes, such as documentation, code analysis, and code generation. Java provides several built-in annotations, and developers can also create their own custom annotations. Java annotations starts with '@'.

Example:
```java
@Deprecated
public class OldClass {
  // code here
}

public @interface MyAnnotation {
    String value() default "default value";
}

//Usage of a custom annotation:
@MyAnnotation(value = "custom value")
public class MyClass {
  // code here
}
```

### Exception Handling:
Java exception handling is the process of catching and handling errors that occur during program execution. When an exception occurs, it is thrown by the program and can be caught and handled by a try-catch block. Java provides a hierarchy of exception classes that can be used to catch different types of exceptions. There can be single or multiple catch block under a try statement. Also after try-catch we can have a finally block which will be executed last.

Example:
```java
try {
  // code that may throw an exception
} catch (ExceptionType1 e) {
  // handle exception type 1
} catch (ExceptionType2 e) {
  // handle exception type 2
} finally {
  // code that will always execute, regardless of whether an exception was thrown or caught
}
```

When we are working with resources or files than java try-catch with resources feature ensures that after all the work automatically closes any resources that are opened in the try block, whether or not an exception occurs.

Example:
```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    System.err.println("Error reading file: " + e.getMessage());
}
```

### Lambda Expression:
Lambda expressions are a shorthand way to define anonymous functions in Java. They can be used to create functional interfaces, which are interfaces that have only one abstract method. Lambda expressions are used to write more concise and readable code, especially when working with streams and collections. It can be single as well as multiline too. It declare with 0 or more parameters followed by '->' and body.

Example:
```java
// Using a lambda expression to define a Comparator for sorting strings by length
// comparator lambda: (s1, s2) -> s1.length() - s2.length()

List<String> strings = Arrays.asList("apple", "banana", "orange", "kiwi");
Collections.sort(strings, (s1, s2) -> s1.length() - s2.length());
System.out.println(strings);
```

### Interfaces:
Define contracts for classes. Means it defines the definition of methods not the actual implementation.

Example:
```java
interface Flyable{ 
    void fly(); 
}

class Bird implements Flyable{ 
    public void fly(){
        System.out.println("Flying");
    }
}
```

### Abstract Class:
Partially implemented base class.

Example:
```java
abstract class Shape{ 
    abstract double area(); 
}
```

Both interface and abstract class are use for achiving abstraction.

### Records:
Compact immutable data class. Means like object of a class type, record types can't update after declaration.

Example:
```java
record Point(int x,int y){}
Point p = new Point(1,2);
```

### Generics:
Type-safe reusable classes. Means we can create classes and use it for multple types based on need.

Example:
```java
class Box<T>{ 
    T value; 
    Box(T v){
        value=v;
    }
}

Box<String> b = new Box<>("Hi");
```

### Module System:
Organize large projects. Declares the dependency beforehand.

Example:
```java
module my.app { 
    requires java.sql; 
    exports com.example; 
}
```

### Reflections:
Inspect classes at runtime.

Example:
```java
Class<?> c = String.class; 
System.out.println(c.getMethods().length);
```
---

*Insha Allah, in the upcoming part, I will try to share the Thread Programming of Java. Until than, may Allah keep you healthy and happy.*