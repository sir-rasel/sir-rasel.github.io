---
title: "Software Design Patterns and Principles - Part 8 (Decorator Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-08"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "decorator-design-pattern"]
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
    image: "img/blogs/51-decorator.png"
    caption: "Decorator Design Pattern"
    alt: "Decorator Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 7:** [Software Design Patterns and Principles - Part 7 (Adapter Design Pattern)]({{< ref "blogs/50-adapter-design-pattern.md" >}})
- **Part 9:** [Software Design Patterns and Principles - Part 9 (Composite Design Pattern)]({{< ref "blogs/52-composite-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/51-decorator.png"
    caption="Decorator Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the decorator design pattern.

So let's get started...

---

## Story
Neela starts a bakery app called "**Decorated Cake App.**" Here he takes orders for different predefined delicious cakes. His app offers vanilla, chocolate, and other types of cake. Day by day, his app and cake become famous and popular. Now people propose and order cake with their preference and want cake decorated in a more elaborate way with extra functionality. So now, Neela needs to adjust his cake with extra functionality without breaking his existing system. As decorations are based on people's choices, day by day more and more versatile preferences will come into the scenario, and Neela needs to adjust to those as well. Here Neela is in tension, wondering how he can achieve such cases in an optimized way.

## Adapter Design Pattern
**Definition**:
> Decorator is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

As the definition states, the decorator pattern helps us to adapt the new functionality along with the existing one. In this pattern a ***Wrapper*** object composites the **Wrappe** object and adds new functionality or decoration on top of the Wrappe object. So the question is, if any object adds extra functionality on top of the existing one, will it be considered a decorator pattern? The answer is no. When the Wrapper class and the Wrapped class both implement the same interface, then it will be called the decorator pattern.

**Problem**:

In the above story, Neela struggles with the additional features or decoration request of his existing cake. Though customization of cake will make his business stronger. Other example scenarios also highlight the attachment of additional functionality.

Other programming problems can be:
- **Text Formatting in a Word Processor**: Imagine you're building a word processor application. You might have a base text object that represents plain text. You can use the decorator pattern to add additional formatting options like bold, italic, underline, etc. Each decorator adds a specific formatting feature without altering the original text object.
- **Coffee Ordering System**: In a coffee ordering system, you might have a base coffee class representing a simple cup of coffee. You can then use decorators to add extra ingredients like milk, sugar, whipped cream, flavor syrups, etc. Each decorator adds a new feature or modification to the original coffee order.
- **Logging in a Web Application**: Suppose you're developing a web application and you want to add logging functionality to certain operations. Instead of directly modifying the code of these operations, you can use the decorator pattern to dynamically add logging behavior to them. This way, you can easily turn logging on or off as needed without changing the core functionality of the operations.
- **Authentication in an API**: In an API service, you might have a base authentication method. Using the decorator pattern, you can add additional layers of authentication such as OAuth, JWT, API key validation, etc. These decorators can be stacked on top of each other to provide multiple layers of security without modifying the original authentication method.
- **Vehicle Customization in a Car Dealership System**: In a car dealership system, you might have a base vehicle class representing a standard model of a car. Using the decorator pattern, you can add customization options like leather seats, sunroofs, alloy wheels, etc. Each decorator adds a different customization option to the base vehicle without altering its fundamental structure.

All of them need to extend the existing functionality without breaking the current one.

**Solution**:

From the above definition of the decorator pattern, it gives us the power of attaching or addingextra functionality on top of existing functionality without breaking the current system. As we can see from the story and above problem statements, the root problem or cause is the enhancements of functionality. So all the scenarios are the perfect example of the use cases of the decorator pattern. We can use or implement the decorator pattern as a solution to the problems stated in earlier sections.

For example, Neela can use a cake decorator to decorate his plain cake with customer preferences and so on...

**UML Diagram**:
{{< figure
    src="/img/blogs/51-decorator-uml.png"
    caption="UML of Decorator Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in the UML diagram we can see that the **Decorator** and **ConcreteComponent** implement the same interface, **Component**. As mentioned earlier, as the decorator class and main component class implement the same interface, that's why our system remains functional and they can be interchangeable. **ConcreteDecorator** is the concrete class with decorator functionality.

**When To Use**:
- Use the Decorator pattern when you need to be able to assign extra behaviors to objects at runtime without breaking the code that uses these objects.
- Use the pattern when it’s awkward or not possible to extend an object’s behavior using inheritance.

**Implementation**:
```java
// Source: Refactoring.com
import java.io.*;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Base64;
import java.util.zip.Deflater;
import java.util.zip.DeflaterOutputStream;
import java.util.zip.InflaterInputStream;

public interface DataSource {
    void writeData(String data);

    String readData();
}

public class FileDataSource implements DataSource {
    private String name;

    public FileDataSource(String name) {
        this.name = name;
    }

    @Override
    public void writeData(String data) {
        File file = new File(name);
        try (OutputStream fos = new FileOutputStream(file)) {
            fos.write(data.getBytes(), 0, data.length());
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
    }

    @Override
    public String readData() {
        char[] buffer = null;
        File file = new File(name);
        try (FileReader reader = new FileReader(file)) {
            buffer = new char[(int) file.length()];
            reader.read(buffer);
        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }
        return new String(buffer);
    }
}

public class DataSourceDecorator implements DataSource {
    private DataSource wrappee;

    DataSourceDecorator(DataSource source) {
        this.wrappee = source;
    }

    @Override
    public void writeData(String data) {
        wrappee.writeData(data);
    }

    @Override
    public String readData() {
        return wrappee.readData();
    }
}

public class EncryptionDecorator extends DataSourceDecorator {

    public EncryptionDecorator(DataSource source) {
        super(source);
    }

    @Override
    public void writeData(String data) {
        super.writeData(encode(data));
    }

    @Override
    public String readData() {
        return decode(super.readData());
    }

    private String encode(String data) {
        byte[] result = data.getBytes();
        for (int i = 0; i < result.length; i++) {
            result[i] += (byte) 1;
        }
        return Base64.getEncoder().encodeToString(result);
    }

    private String decode(String data) {
        byte[] result = Base64.getDecoder().decode(data);
        for (int i = 0; i < result.length; i++) {
            result[i] -= (byte) 1;
        }
        return new String(result);
    }
}

public class CompressionDecorator extends DataSourceDecorator {
    private int compLevel = 6;

    public CompressionDecorator(DataSource source) {
        super(source);
    }

    public int getCompressionLevel() {
        return compLevel;
    }

    public void setCompressionLevel(int value) {
        compLevel = value;
    }

    @Override
    public void writeData(String data) {
        super.writeData(compress(data));
    }

    @Override
    public String readData() {
        return decompress(super.readData());
    }

    private String compress(String stringData) {
        byte[] data = stringData.getBytes();
        try {
            ByteArrayOutputStream bout = new ByteArrayOutputStream(512);
            DeflaterOutputStream dos = new DeflaterOutputStream(bout, new Deflater(compLevel));
            dos.write(data);
            dos.close();
            bout.close();
            return Base64.getEncoder().encodeToString(bout.toByteArray());
        } catch (IOException ex) {
            return null;
        }
    }

    private String decompress(String stringData) {
        byte[] data = Base64.getDecoder().decode(stringData);
        try {
            InputStream in = new ByteArrayInputStream(data);
            InflaterInputStream iin = new InflaterInputStream(in);
            ByteArrayOutputStream bout = new ByteArrayOutputStream(512);
            int b;
            while ((b = iin.read()) != -1) {
                bout.write(b);
            }
            in.close();
            iin.close();
            bout.close();
            return new String(bout.toByteArray());
        } catch (IOException ex) {
            return null;
        }
    }
}

public class Demo {
    public static void main(String[] args) {
        String salaryRecords = "Name,Salary\nJohn Smith,100000\nSteven Jobs,912000";
        DataSourceDecorator encoded = new CompressionDecorator(
                                         new EncryptionDecorator(
                                             new FileDataSource("out/OutputDemo.txt")));
        encoded.writeData(salaryRecords);
        DataSource plain = new FileDataSource("out/OutputDemo.txt");

        System.out.println("- Input ----------------");
        System.out.println(salaryRecords);
        System.out.println("- Encoded --------------");
        System.out.println(plain.readData());
        System.out.println("- Decoded --------------");
        System.out.println(encoded.readData());
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Structural%20Design%20Pattern/DecoratorDesignPattern/C%23).

---

## Achieved Design Principles:
- **Open/Closed Principle (OCP)**: This principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, you should be able to add new functionality or behavior to a system without altering the existing code.
- **Single Responsibility Principle (SRP)**: Each decorator class has a single responsibility, which is to modify the behavior of the wrapped component. This helps in keeping classes focused on doing one thing and doing it well.
- **Composition over Inheritance**: Instead of relying on subclassing and inheritance to add functionality, the Decorator pattern emphasizes composition. It allows you to compose objects with different behaviors dynamically at runtime, promoting greater flexibility and avoiding the issues associated with deep class hierarchies.
- **Interface Segregation Principle (ISP)**: Clients interact with the component interface and do not need to know about the decorators' concrete implementations. This prevents clients from depending on methods they do not use, adhering to the ISP.
- **Dependency Inversion Principle (DIP)**: By depending on abstractions (interfaces or abstract classes) rather than concrete classes, the Decorator pattern follows the DIP. This allows for easier substitution of components and promotes loosely coupled designs.
- **Encapsulation**: Each decorator encapsulates the behavior it adds to the wrapped component. This encapsulation ensures that changes in one decorator do not affect others or the base component, maintaining modularity and reducing unintended side effects.
- **Flexibility and Extensibility**: The Decorator pattern allows you to add or remove responsibilities (decorators) dynamically at runtime. This flexibility makes it easy to customize the behavior of objects without modifying their underlying classes, promoting extensibility.
- **Maintainability**: By separating concerns and keeping the core component and decorators decoupled, the Decorator pattern improves code maintainability. Changes in behavior can be made by adding or modifying decorators, rather than modifying existing classes, reducing the risk of introducing bugs.