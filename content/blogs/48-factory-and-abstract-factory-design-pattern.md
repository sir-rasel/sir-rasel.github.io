---
title: "Software Design Patterns and Principles - Part 5 (Factory Method and Abstract Factory Method Design Pattern)"
description: "Let's learn the software and oop design patterns and principles!"
date: 2025-10-30
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "factory-design-pattern", "abstract-factory-design-pattern"]
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
    image: "img/blogs/48-factory.png"
    caption: "Factory Method Design Pattern"
    alt: "Factory Method Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 4:** [Software Design Patterns and Principles - Part 4 (Singleton Design Pattern)]({{< ref "blogs/46-singleton-design-pattern.md" >}})
- **Part 6:** [Software Design Patterns and Principles - Part 6 (Builder Design Pattern)]({{< ref "blogs/49-builder-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/48-factory.png"
    caption="Factory Method Design Pattern (Photo Credit: Google)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the factory method and abstract factory method design pattern.

So let's get started...

---

## Story
Rakib starts a computer processor distributing company. Below is the journey of his company at a glance:
- Phase 1: At the beginning of his company, he only distributed Intel processors. But as his company grows up and becomes popular day by day, he starts distributing other companies' processors as well.
- Phase 2: After some years his company became larger than before, and they started distributing personal computers by assembling all parts by brand.

## Factory Method Design Pattern
**Definition**:
> Factory Method is a creational design pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created.

From the definition we can see that the factory method design pattern, as its name suggests, provides a method that is responsible for creating objects and is part of the superclass. And also it allows overriding the method to its subclass so that subclass can create different types of objects based on their needs. But how can a method return different types? It does not return a concrete class but an interface type that the concrete class implements.

**Problem**:

In the above story at phase 1, first Rakib starts distributing Intel processors. Say Rakib's implement in his system is an **IntelProcessor** class. So he can create this type of object only using just new **IntelProcessor**(). But when his business grows and he starts distributing many other different companies' processors, how can he accommodate his system implementation? Is it feasible to create every company's processor differently using a **new** operator from a different place in the codebase or just centralize it? Here the factory method design pattern is the rescuer.

**Solution**:

As I said, the factory method design pattern is one of the solutions. We will create an interface called "processor," and all other company's concrete processor classes will implement the processor interface. Also, instead of calling new for creating an object, we will use a factory method called **getProcessor**() for getting processor objects based on company. That's how we can organize our code as reusable and solve our growing problem.

**UML Diagram**:
{{< figure
    src="/img/blogs/48-factory-uml.gif"
    caption="UML of Factory Method Design Pattern (Photo Credit: Google)"
    align=center
>}}

Here in the UML diagram, we see that when the creator calls the **FactoryMethod**(), it gets a common interface type of **Product**. And **ConcreteCreator** returns a **ConcreteProduct**, which implements the **Product**. That way, different **ConcreteCreator** and **ConcreteProduct** can be extended over time.

**When To Use**:
1. Use the factory method pattern when you don't know beforehand the exact types and dependencies of the objects your code should work with.
2. Use the pattern when you want to provide users of your library or framework with a way to extend its internal components.
3. Use the pattern when you want to save system resources by using existing objects instead of rebuilding them each time.

**Implementation**:
```java
interface Processor {
    int getRegisterMemorySize();
}

class IntelProcessor implements Processor {
    private int registerMemorySize;

    public IntelProcessor(int size) {
        this.registerMemorySize = size;
    }

    @Override
    public int getRegisterMemorySize() {
        return registerMemorySize;
    }
}

class AmdProcessor implements Processor {
    private int registerMemorySize;

    public AmdProcessor(int size) {
        this.registerMemorySize = size;
    }

    @Override
    public int getRegisterMemorySize() {
        return registerMemorySize;
    }
}

public class FactoryMethodDemo {
    public static void main(String[] args) {
       
        String processorInput = args[0];
        String processorType = processorInput.substring(processorInput.indexOf('.') + 1,(processorInput.length()));

        Processor processor;
        if (processorType.equals("intel")) {
            processor = new IntelProcessor(1024);
        }
        if (processorType.equals("amd")) {
            processor = new AmdProcessor(512);
        }

        int size = processor.getRegisterMemorySize();
        System.out.println(size);
    }
}
```
Another C# implementation of factory method design pattern find [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Creational%20Design%20Pattern/FactoryMethodDesignPattern/C%23).

---

## Abstract Factory Method Design Pattern
**Definition**:
> Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.

From the definition we can see that the abstract factory method design pattern, as its name suggests, provides a factory class, and this factory class contains one or more factory methods that return different types of objects but conceptually related objects.

**Problem**:

In the above story at phase 2, Rakib starts distributing not only processors but also personal computers by assembling different parts by brand. Say Rakib implements in his system an **IntelComputerFactory** class. So he can create this type of object only using just new **IntelComputerFactory**(). And inside this class, all other computer parts classes are implemented by the Intel company. But as of now, Rakib not only deals with the Intel company, so how can he accommodate other companies as well? Here the abstract factory method design pattern is the rescuer.

**Solution**:

As I said, the abstract factory method design pattern is one of the solutions. We will create an interface called AbstractComputer, and all other company's concrete factory classes will implement the AbstractComputer interface. Then the client class object is called and initializes the factory at run time based on the company type that is going to be built. Also concrete computer factory classes will contain methods for creating computer parts products. That's how we can organize our code as reusable and solve our co-related product creation problem.

**UML Diagram**:
{{< figure
    src="/img/blogs/48-abstract-factory-uml.png"
    caption="UML of Abstract Factory Method Design Pattern (Photo Credit: Google)"
    align=center
>}}

Here in the UML diagram, we see that the client calls and initializes **AbstractFactory** based on the type of product it wants. **ConcreteFactory** deals with the **Product**. Different factories deal with different variants of products. So with the change of factory, product type and variant are also changed automatically.

**When To Use**:
1. Use the pattern when your code needs to create groups of related objects or families of related objects dynamically.
2. Use the pattern when your code needs to work with various families or related objects, but you don't want it to depend on the concrete classes of these objects—they might be unknown beforehand, or you simply want to allow for future extensibility.

**Implementation**:
```java
abstract class Processor {}

class IntelProcessor extends Processor {}

class AsusProcessor extends Processor {}

abstract class Ram {}

class IntelRam extends Ram {}

class AsusRam extends Ram {}

abstract class AbstractFactory {
    private static final IntelFactory intelFactory = new IntelFactory();
    private static final AsusFactory asusFactory = new AsusFactory();

    static AbstractFactory getFactory(Architecture architecture) {
        AbstractFactory factory = null;
        switch (company) {
            case INTEL:
                factory = intelFactory;
                break;
            case ASUS:
                factory = asusFactory;
                break;
        }
        return factory;
    }

    public abstract Processor createProcessor();
    public abstract Ram createRam();
}

class IntelFactory extends AbstractFactory {
    @Override
    public Processor createProcessor() {
        return new IntelProcessor();
    }

    @Override
    public Ram createRam() {
        return new IntelRam();
    }
}

class AsusFactory extends AbstractFactory {
    @Override
    public Processor createProcessor() {
        return new AsusProcessor();
    }

    @Override
    public RAM createRam() {
        return new AsusRam();
    }
}

enum Company {
    INTEL, ASUS
}

public class Client {
    public static void main(String[] args) {
        AbstractFactory factory = AbstractFactory.getFactory(Company.ASUS);
        CPU cpu = factory.createCPU();
    }
}
```
Another C# implementation of abstract factory method design pattern find [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Creational%20Design%20Pattern/AbstractFactoryDesignPattern/C%23).

---

## Difference and When Use What:
> The Factory Method pattern deals with creating objects of a single type, while the Abstract Factory pattern deals with creating objects of related types.

As we saw earlier in our above discussion, the factory method offers a method for creating objects. Single object and single type per method.

On the other hand, an abstract factory, itself a factory object, offers multiple methods for object creation and related object creation.

> The main difference between Abstract Factory and Factory Method is that **Abstract Factory is implemented by composition, but Factory Method is implemented by inheritance**.

As we also see earlier in our above discussion, the factory method allows us to override the method to its subclasses and change the created object type from the base class. So we see here an inheritance relationship.

On the other hand, an abstract factory is a factory composed of object properties in a client class that allow you to change the factory and create related objects. So we see here a composition relationship.

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: We can achieve SRP by these design patterns. Because different factories and product classes can contain their own responsibilities.
- **Open/Closed Principle (OCP)**: We can achieve OCP by these design patterns. Because we can extend and create a new class for adding responsibility without modifying the existing ones.
- **Interface Segregation Principle (ISP)**: We can achieve IS by these design patterns. Because different factories and product classes depend on different interfaces.