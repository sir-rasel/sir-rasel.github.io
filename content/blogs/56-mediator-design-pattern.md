---
title: "Software Design Patterns and Principles - Part 13 (Mediator Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-15T01:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "mediator-design-pattern"]
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
    image: "img/blogs/56-mediator.png"
    caption: "Mediator Design Pattern"
    alt: "Mediator Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 12:** [Software Design Patterns and Principles - Part 12 (Command Design Pattern)]({{< ref "blogs/55-command-design-pattern.md" >}})
- **Part 14:** [Software Design Patterns and Principles - Part 14 (Observer Design Pattern)]({{< ref "blogs/57-observer-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/56-mediator.png"
    caption="Mediator Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the mediator design pattern.

So let's get started...

---

## Story
Once upon a time there was a programming club called "Chaotic Programming Club." There were several roles, and people with these roles were holders in the club committee. So as there were multiple roles and multiple people in the club committee, the problem began there. To do work or make a decision, there was a chaotic dependency; some people need to discuss or have dependency on each other. So the situation was not so good or friendly. They feel the need for a central collaboration or reduction of direct communication very badly.

## Mediator Design Pattern
**Definition**:
> Mediator is a behavioral design pattern that lets you reduce chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.

As the definition states, the mediator design pattern offers a centralized communication option between multiple objects without them knowing each other. When multiple objects call or interact with each other, they create chaotic dependencies and tight coupling. So the mediator pattern introduces a mediator object, which is responsible for all collaboration and communication between objects without direct access to each other.

**Problem**:

In the above story, the direct communication between multiple people is not good and creates a chaotic dependency. They need to reduce the dependency. But how will they do that?

The mediator design pattern can be beneficial in various scenarios where there's a need for centralized communication and coordination between multiple objects or components. Here are some common scenarios where the mediator pattern can be effectively applied:
- **Chat Applications**: As illustrated in the short story earlier, chat applications often involve multiple users communicating with each other through various message types (text, images, files). A mediator can manage the exchange of messages between users, handling message routing, notifications, and other communication-related tasks.
- **GUI Components**: In graphical user interfaces (GUI), different components such as buttons, text fields, and dropdown menus may need to interact with each other based on user actions. A mediator can facilitate communication between these components, handling events and orchestrating their behavior.
- **Flight Control System**: In a flight control system, various subsystems such as navigation, altitude control, and communication systems need to coordinate their actions to ensure safe and efficient flight operations. A mediator can oversee the interaction between these subsystems, managing data exchange, decision-making, and system integration.
- **Online Marketplace**: In an online marketplace platform, multiple entities such as buyers, sellers, and payment processors need to interact with each other to facilitate transactions. A mediator can serve as an intermediary, managing order processing, inventory updates, payment verification, and communication between parties.
- **Multiplayer Games**: In multiplayer games, players interact with each other and with game elements such as characters, objects, and environments. A mediator can handle player actions, game events, and synchronization between clients and servers, ensuring smooth gameplay and a consistent game state.
- **Distributed Systems**: In distributed systems comprising multiple nodes or services, coordination and communication between components are essential for achieving desired functionality and performance. A mediator can facilitate interaction between distributed components, managing message passing, synchronization, and fault tolerance.
- **Event-driven Architectures**: In event-driven architectures where components react to events triggered by various sources, a mediator can act as a central event bus or dispatcher. It routes events to interested subscribers, coordinates event handling, and facilitates communication between event producers and consumers.
- **Workflow Management Systems**: In workflow management systems where tasks need to be coordinated across multiple steps or participants, a mediator can orchestrate workflow execution, manage task dependencies, and handle exceptions or escalations.

In all these scenarios, the mediator pattern helps promote modularity, decoupling, and maintainability by centralizing communication logic and isolating interaction concerns from individual components or subsystems.

**Solution**:

In the above story, they feel the urgency of a central collaboration or centralized communication very badly. So they will appoint a communication manager who will be responsible for all communication. So people will not collaborate directly with each other. They just inform the manager, and the manager will handle the rest of the communication to other necessary people. Here the communication manager is the mediator.

We can also use or implement the mediator pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/56-mediator-uml.png"
    caption="UML of Mediator Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

Here in the UML diagram we can see that the **ConcreteMediator** class implements the **Mediator** interface, and the other related **Component** class holds a reference to **Mediator**. So when a **Component** does an **operation**(), then he just **notify**() the mediator. Then the mediator interacts with other components if necessary based on the condition, as it holds other components' references as well.

It's often practiced that the mediator design pattern is implemented using the observer design pattern for notifying components.

**When To Use**:
- Use the Mediator pattern when it’s hard to change some of the classes because they are tightly coupled to a bunch of other classes.
- Use the pattern when you can’t reuse a component in a different program because it’s too dependent on other components.
- Use the Mediator when you find yourself creating tons of component subclasses just to reuse some basic behavior in various contexts.

**Implementation**:
```java
import java.util.ArrayList;
import java.util.List;

// Mediator Interface
interface ChatMediator {
    void sendMessage(String message, User user);
    void addUser(User user);
}

// Concrete Mediator
class ChatMediatorImpl implements ChatMediator {
    private List<User> users;

    public ChatMediatorImpl() {
        this.users = new ArrayList<>();
    }

    @Override
    public void sendMessage(String message, User user) {
        for (User u : users) {
            // Exclude the sender
            if (u != user) {
                u.receiveMessage(message);
            }
        }
    }

    @Override
    public void addUser(User user) {
        users.add(user);
    }
}

// Colleague Interface
abstract class User {
    protected ChatMediator mediator;
    protected String name;

    public User(ChatMediator mediator, String name) {
        this.mediator = mediator;
        this.name = name;
    }

    public abstract void sendMessage(String message);
    public abstract void receiveMessage(String message);
}

// Concrete Colleague
class BasicUser extends User {
    public BasicUser(ChatMediator mediator, String name) {
        super(mediator, name);
    }

    @Override
    public void sendMessage(String message) {
        System.out.println(name + " sends: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receiveMessage(String message) {
        System.out.println(name + " receives: " + message);
    }
}

public class MediatorPatternExample {
    public static void main(String[] args) {
        ChatMediator mediator = new ChatMediatorImpl();

        User user1 = new BasicUser(mediator, "User 1");
        User user2 = new BasicUser(mediator, "User 2");
        User user3 = new BasicUser(mediator, "User 3");

        mediator.addUser(user1);
        mediator.addUser(user2);
        mediator.addUser(user3);

        user1.sendMessage("Hello, everyone!");
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Behavioral%20Design%20Pattern/MediatorPatternUsingObserverPattern/C%23).

---

## Achieved Design Principles:
- **Encapsulation**: The mediator encapsulates the communication logic between objects, hiding the details of their interactions. This promotes encapsulation by restricting direct access to object internals and providing a clear interface for communication.
- **Abstraction**: By providing a central mediator interface, the pattern abstracts the details of how objects interact with each other. This abstraction allows developers to focus on high-level interactions rather than low-level implementation details, promoting a cleaner and more maintainable design.
- **Single Responsibility Principle (SRP)**: The mediator class has the responsibility of mediating communication between objects, adhering to the SRP. Each object has a single responsibility, and the mediator handles the coordination between them, ensuring that classes have a single reason to change.
- **Loose Coupling**: Objects in a system employing the mediator pattern are loosely coupled since they communicate through the mediator rather than directly with each other. This loose coupling reduces dependencies between objects, making the system more flexible and easier to maintain.
- **Separation of Concerns**: The mediator separates the concerns of communication from the individual objects. Objects are responsible for their specific functionality, while the mediator is responsible for coordinating their interactions. This separation promotes modularity and enhances the maintainability of the system.
- **Open/Closed Principle (OCP)**: The mediator pattern supports the Open/Closed Principle by allowing the system to be easily extended with new types of objects or behaviors. New objects can be integrated into the system without modifying existing objects, as long as they adhere to the mediator interface.
- **Modularity**: The mediator pattern promotes modularity by encapsulating the interaction logic within a separate mediator class. This modularity makes it easier to understand, maintain, and extend the system by isolating changes related to communication from other parts of the system.
- **Simplification of Communication**: The mediator pattern simplifies communication between objects by providing a centralized point for interaction. This makes it easier to understand and maintain the system, as developers don't have to track numerous interconnections between objects.
- **Promotion of Reusability**: With the mediator handling communication, individual objects can remain more focused on their specific tasks. This promotes reusability since objects can be easily integrated into different contexts without significant changes.
- **Encapsulation of Interaction Logic**: The mediator encapsulates the logic for how objects interact with each other. This encapsulation shields the participating objects from the details of each other's implementations, promoting better encapsulation and abstraction.
- **Scalability**: The mediator pattern facilitates the addition of new components or functionalities to a system without affecting existing ones. This scalability is achieved by ensuring that new components can communicate through the mediator without needing modifications to existing components.