---
title: "Software Design Patterns and Principles - Part 14 (Observer Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-15T03:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "observer-design-pattern"]
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
    image: "img/blogs/57-observer.jpg"
    caption: "Observer Design Pattern"
    alt: "Observer Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 13:** [Software Design Patterns and Principles - Part 13 (Mediator Design Pattern)]({{< ref "blogs/56-mediator-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/57-observer.jpg"
    caption="Observer Design Pattern (Photo Credit: Webmobtuts)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the observer design pattern.

So let's get started...

---

## Story
Roni is the owner of a confectionery shop near a girls' school. There he sells chocolate, sweets, ice cream, and other things. Rina is a student of class 10 of this girls' school who often visits Roni's shop for buying ice cream and chocolate. Anik is a neighbor of Roni who likes Rina a lot. As a result, Anik frequently visits Roni's shop and continuously asks about Rina: Has he come? When will he come? etc. Here, not only Anik, but also some other little brothers often disturb Roni. So after some days the situation got very serious, and Roni told Anik and others to give him their phone numbers so that he could inform them when Rina and others visited his shop.

## Observer Design Pattern
**Definition**:
> Observer is a behavioral design pattern that lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.

As the definition states, the observer design pattern gives a subscription mechanism where one or more objects can subscribe to a publisher object, and when any change happens, then the publisher can notify the subscriber object about the changes. Also, a subscriber can unsubscribe at any time if it wants. So subscriber objects observe the publisher object and react based on it.

**Problem**:

In the above story, Roni got disturbed, and the situation is not so nice for Anik and others with the continuous knocking. So he needs a solution by which anyone not knocking him will inform others. How can this be achieved?

The observer design pattern is a widely used pattern in software engineering for implementing distributed event handling systems, in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them of any state changes, usually by calling one of their methods. Here are some scenarios where the observer design pattern can be applied:
- **User Interface Components**: In graphical user interfaces (GUIs), various UI components such as buttons, checkboxes, and sliders often need to react to changes in other components or underlying data. Observers can be used to notify these components of changes, ensuring synchronization and consistency in the UI.
- **Event Handling Systems**: In event-driven systems, such as web applications or games, there are often multiple events occurring simultaneously that need to be handled by different parts of the system. Observers can be employed to listen for specific events and trigger appropriate actions or responses.
- **Publish-Subscribe Systems**: In systems where publishers produce data or events and subscribers consume them, the observer pattern can be used to implement the pub-sub mechanism. Publishers notify subscribers about new data or events, allowing for loose coupling between components.
- **Model-View-Controller (MVC) Architecture**: The observer pattern is a fundamental part of the MVC architecture, where the model represents the data, the view represents the presentation, and the controller acts as an intermediary between them. Views observe changes in the model and update their presentation accordingly.
- **Databases and Cache Invalidation**: In distributed systems with caching mechanisms, changes to data stored in databases need to be reflected in cached copies. Observers can be employed to notify cache instances of data changes, ensuring that cached data remains consistent with the database.
- **Sensor Networks and IoT**: In sensor networks and Internet of Things (IoT) applications, sensors often produce data that needs to be monitored and acted upon in real-time. Observers can be used to track sensor readings and trigger alerts or actions based on predefined thresholds.
- **Stock Market or Financial Systems**: In systems that deal with real-time financial data, such as stock market applications, observers can be used to monitor changes in stock prices, currency exchange rates, or other financial metrics and notify interested parties, such as traders or investors.

Overall, the observer pattern provides a flexible and efficient way to handle communication and coordination between different components of a system, making it a valuable tool in various software development scenarios.

**Solution**:

In the above story, Roni asked for the phone numbers of Anik and others. So Anik and others give him their phone numbers and tell him to call when their liked person visits his shop. So Roni here is the subject/publisher who will inform about the event (here the event is Rina and other girls). And Anik and other boys are subscribers who subscribe to Roni by giving their phone number. So as a result, the observer pattern solves their problem.

We can also use or implement the observer pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/57-observer-uml.png"
    caption="UML of Observer Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in the UML diagram we can see that there can be multiple **ConcreteObservers** who are implementing the common **Observer** interface. Then a **Subject** class, which is mainly the publisher, holds the observer list and gives an attach and detach mechanism for observers in the subscription list. So when any event happens on the subject, it immediately publishes or notifies the observer objects.

**When To Use**:
- Use the Observer pattern when changes to the state of one object may require changing other objects, and the actual set of objects is unknown beforehand or changes dynamically.
- Use the pattern when some objects in your app must observe others, but only for a limited time or in specific cases.

**Implementation**:
```java
import java.util.ArrayList;
import java.util.List;

// Subject interface
interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// Concrete Subject class
class WeatherStation implements Subject {
    private int temperature;
    private List<Observer> observers;

    public WeatherStation() {
        observers = new ArrayList<>();
    }

    public void setTemperature(int temperature) {
        this.temperature = temperature;
        notifyObservers();
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature);
        }
    }
}

// Observer interface
interface Observer {
    void update(int temperature);
}

// Concrete Observer classes
class PhoneDisplay implements Observer {
    @Override
    public void update(int temperature) {
        System.out.println("Phone Display: Current temperature is " + temperature + " degrees Celsius.");
    }
}

class LaptopDisplay implements Observer {
    @Override
    public void update(int temperature) {
        System.out.println("Laptop Display: Current temperature is " + temperature + " degrees Celsius.");
    }
}

public class ObserverPatternExample {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();

        PhoneDisplay phoneDisplay = new PhoneDisplay();
        LaptopDisplay laptopDisplay = new LaptopDisplay();

        weatherStation.registerObserver(phoneDisplay);
        weatherStation.registerObserver(laptopDisplay);

        // Simulate temperature change
        weatherStation.setTemperature(25);

        // Unregister laptop display
        weatherStation.removeObserver(laptopDisplay);

        // Simulate temperature change again
        weatherStation.setTemperature(30);
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Behavioral%20Design%20Pattern/ObserverDesignPattern/C%23).

---

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: The Subject class is responsible for maintaining a list of observers and notifying them of changes. The Observer interface or base class defines the contract for observers without dictating their implementation details. This separation of concerns ensures that each class has a single responsibility, enhancing maintainability and flexibility.
- **Open/Closed Principle (OCP)**: The Observer pattern allows for the addition of new observers without modifying the subject class. Subjects can notify any number of observers without needing to know their specific implementations. This promotes code extensibility and reduces the risk of introducing bugs when extending the system.
- **Liskov Substitution Principle (LSP)**: Observers can be substituted with different concrete observer implementations without affecting the behavior of the subject. New types of observers can be introduced as long as they adhere to the contract defined by the Observer interface or base class. This principle ensures that derived classes (observers) can be used interchangeably with their base class (Observer), preserving program correctness.
- **Dependency Inversion Principle (DIP)**: Subjects depend on abstractions (Observer interface or base class) rather than concrete observer implementations. Observers depend on the subject interface rather than the specific implementation of the subject. This promotes loose coupling between subject and observer classes, making the system more flexible and easier to maintain.
- **Encapsulation**: The Observer pattern encapsulates the communication logic between subjects and observers within the subject class. Observers are isolated from each other and interact with the subject through a well-defined interface. This encapsulation enhances modularity and reduces the risk of unintended interactions between components.
- **Separation of Concerns**: The Observer pattern separates the concerns of data management (subject) from behavior (observers). Subjects focus on managing state and notifying observers, while observers focus on responding to state changes. This separation facilitates code organization, readability, and maintenance.