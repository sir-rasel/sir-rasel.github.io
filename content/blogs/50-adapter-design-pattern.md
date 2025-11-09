---
title: "Software Design Patterns and Principles - Part 7 (Adapter Design Pattern)"
description: "Let's learn the software and oop design patterns and principles!"
date: "2025-11-05T03:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "adapter-design-pattern"]
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
    image: "img/blogs/50-adapter.jpeg"
    caption: "Adapter Design Pattern"
    alt: "Adapter Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 6:** [Software Design Patterns and Principles - Part 6 (Builder Design Pattern)]({{< ref "blogs/49-builder-design-pattern.md" >}})
- **Part 8:** [Software Design Patterns and Principles - Part 8 (Decorator Design Pattern)]({{< ref "blogs/51-decorator-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/50-adapter.jpeg"
    caption="Adapter Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the adapter design pattern.

So let's get started...

---

## Story
My friend Sabbir was so frustrated with his life some days ago. Because everywhere, everything he faced was disturbing and not in favor of him. For example, he visits a country where all the sockets are 2-pin for charging electric devices, but his laptop and phone charger need 3-pin sockets. Another case was that he wants to connect a printer, and the port is USB 3.0 type, but his laptop supports only Type-C style cable. Also, another most frustrating scenario was the language barrier problem. His language was not understandable by others, and he also didn't understand the local people. In these types of situations, he wanted to adapt the cases carefully. He adapts and makes his life happy.

## Adapter Design Pattern
**Definition**:
> Adapter is a structural design pattern that allows objects with incompatible interfaces to collaborate. It means working with one type to achieve another different type.

As the definition states, the adapter pattern helps us to adapt to the difference or incompatibility. An **adapter** class can be used as a middlemanor translator of 2 different entities. It acts as a bridge between two incompatible interfaces, converting the interface of one class (the **adaptee**) into another interface that a client expects. This pattern enables objects to collaborate despite differences in their interfaces, promoting code reusability, flexibility, and interoperability.

**Problem**:

In the above story, Sabbir struggles with incompatibility. He faces problems with his phone and laptop charger, with his cable port for the printer, with language differences, etc. The root of all the problems is difference or incompatibility.

Other programming problems can be:
- A system works with XML-format data but now wants to work with JSON format too.
- A system supports the MySQL database but wants to use PostgreSQL now.
- A system that supports a third-party provider now wants to use other third-party APIs.
- A system wants to upgrade its functionality but also wants to be backward compatible with the legacy system.

**Solution**:

From the above definition of the adapter pattern, it gives us the power of compatibility for working with incompatible problems. As we can see from the story and above problem statements, the root problem or cause is the incompatibility. So we can use or implement the adapter pattern as a solution to the problems stated in earlier sections.

For example, Sabbir can use a socket adapter to support his 3-pin ports with 2-pin ports. Also can be used as a USB to Type-C adapter for printer support. A language adapter can be used for 2 different language translations.

Also, a version adapter can be used to upgrade the system but also maintain support for the legacy one. A DB adapter can adopt MySQL and PostgreSQL. And so on...

**UML Diagram**:
{{< figure
    src="/img/blogs/50-adapter-uml.jpeg"
    caption="UML of Adapter Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in the UML diagram, we see 2 different diagrams. Yes, you see it right. Adapter design pattern implementation can be achieved in 2 different ways. One is via **Object Adapter**, and another is called **Class Adapter**.

In an object adapter, the client class is the one who called the required method basically from the interface. The client can be called the **Adaptee** (the main service class) directly or can be called the **Adapter** class object too. The adapter class composes the adaptee class (the main service class) object. So when the adapter class does some operation first, it calls the adaptee class object method and then manipulates the result accordingly before responding to the client.

Object adapter is the most used implementation because it supports all languages, but to achieve a class adapter, we need the support of multiple inheritance like C++.

**When To Use**:
- Use the Adapter class when you want to use some existing class, but its interface isn’t compatible with the rest of your code.
- Use the pattern when you want to reuse several existing subclasses that lack some common functionality that can’t be added to the superclass.

**Implementation**:
```java
public class JsonData {}

public class XmlData {}

public interface MultiRestoApp {
    void displayMenus(XmlData xmlData);
    void displayRecommendations(XmlData xmlData);
}

public class MultiRestoAppImpl implements MultiRestoApp {

    @Override
    public void displayMenus(XmlData xmlData) {
        // Displays menus using XML data
        System.out.println("Displaying Menus using XML data...");
    }

    @Override
    public void displayRecommendations(XmlData xmlData) {
        // Displays recommendations using XML data
        System.out.println("Displaying Recommendations using XML data...");
    }
}

public class FancyUIService {

    public void displayMenus(JsonData jsonData) {
        // Make use of the JsonData to fetch menus
    }

    public void displayRecommendations(JsonData jsonData) {
        // Make use of the JsonData to load recommendations
    }
}

public class FancyUIServiceAdapter implements MultiRestoApp {

    private final FancyUIService fancyUIService;

    public FancyUIServiceAdapter() {
        fancyUIService = new FancyUIService();
    }

    @Override
    public void displayMenus(XmlData xmlData) {
        JsonData jsonData = convertXmlToJson(xmlData);
        System.out.println("Displaying Fancy Menus using converted JSON data...");
        fancyUIService.displayMenus(jsonData);
    }

    @Override
    public void displayRecommendations(XmlData xmlData) {
        JsonData jsonData = convertXmlToJson(xmlData);
        System.out.println("Displaying Fancy Recommendations using converted JSON data...");
        fancyUIService.displayRecommendations(jsonData);
    }

    private JsonData convertXmlToJson(XmlData xmlData) {
        // Converts XmlData to JsonData and return it
        System.out.println("Converting XML to JSON...");
        return new JsonData();
    }
}

public class MainApp {

    public static void main(String[] args) {

        XmlData myData = new XmlData();

        // Old UI
        MultiRestoApp multiRestoApp = new MultiRestoApp();
        multiRestoApp.displayMenus(myData);
        multiRestoApp.displayRecommendations(myData);

        System.out.println("==========================================");

        // New UI
        MultiRestoApp adapter = new FancyUIServiceAdapter();
        adapter.displayMenus(myData);
        adapter.displayRecommendations(myData);
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Structural%20Design%20Pattern/AdapterDesignPattern/C%23).

---

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: The Adapter pattern helps adhere to the SRP by separating concerns. Adapters are responsible for mapping the interface of one class to another, ensuring that each class has a single responsibility: the adapted interface or the original functionality.
- **Open/Closed Principle (OCP)**: The Adapter pattern promotes the OCP by allowing new adapters to be added without modifying the existing client code or the adaptee. This ensures that the system can be extended with new functionality (new adapters) without altering its existing behavior.
- **Dependency Inversion Principle (DIP)**: The Adapter pattern facilitates the DIP by abstracting the dependencies between the client and the adaptee. Instead of the client depending directly on the adaptee, it depends on the adapter interface. This allows for flexibility in swapping different implementations of adapters without affecting the client.
- **Interface Segregation Principle (ISP)**: The Adapter pattern supports the ISP by providing tailored interfaces for clients. Adapters can expose only the methods and properties that are relevant to the client, hiding unnecessary details of the adaptee's interface.
- **Composition over Inheritance**: Instead of relying on inheritance, the Adapter pattern often utilizes composition to achieve its goals. Adapters typically wrap an instance of the adaptee class, allowing for more flexible and manageable code structures compared to inheritance-based solutions.
- **Code Reusability**: By abstracting the interface of the adaptee, the Adapter pattern promotes code reusability. Adapters can be reused across different parts of the system or in different projects where similar adaptation is required.
- **Encapsulation**: Adapters encapsulate the details of adapting one interface to another, shielding the client from the complexities of interacting with the adaptee directly. This promotes encapsulation and information hiding, leading to more maintainable and understandable code.
- **Flexibility and Interoperability**: The Adapter pattern enhances the flexibility and interoperability of systems by allowing components with incompatible interfaces to work together seamlessly. This promotes system integration and facilitates the reuse of existing components in new contexts.