---
title: "Software Design Patterns and Principles - Part 10 (Facade Design Pattern)"
description: "Let's learn the software and oop design patterns and principles!"
date: "2025-11-14"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "facade-design-pattern"]
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
    image: "img/blogs/52-composite.png"
    caption: "Composite Design Pattern"
    alt: "Composite Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 9:** [Software Design Patterns and Principles - Part 9 (Composite Design Pattern)]({{< ref "blogs/52-composite-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/53-facade.png"
    caption="Facade Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the facade design pattern.

So let's get started...

---

## Story
One of my friends, named Rubel, is known as a lover boy among us. Because he maintains lots of girlfriends (at least 5-7) at a time. And you know what? Handling and maintaining a girlfriend is a very complex and time-consuming task. Rubel maintains connections with some of these girlfriends via phone call and some of them via message/chat. Though the pattern of handling the girl is almost the same, day by day it becomes very clumsy and a headache, as he needs to interact with this complex system directly. So now he is planning a way for how he can simplify this complexity.

## Facade Design Pattern
**Definition**:
> A façade is a structural design pattern that provides a simplified interface to a library, a framework, or any other complex set of classes.

As the definition states, the façade pattern helps us to fight with complex unstructured systems. It gives an opportunity to work with a complex system by offering a simple interface. The user or caller needn't be concerned about the complexity of the system; they just use the simple common interface. That's it.

**Problem**:

In the above story, Rubel faces the problem of maintaining a complex system and maintaining or interacting with multiple girls together. So how can he simplify this?

Here are a few scenarios where the Façade pattern can be effectively employed:
- **Complex Subsystem Simplification**: Imagine you're building a multimedia processing application that involves intricate operations like decoding different types of media files, manipulating audio and video streams, and rendering them onto various output devices. Rather than exposing all the complexities of these subsystems directly to the client code, you can create a MultimediaFacade class that offers simple methods like playVideo(), playAudio(), or renderMedia(). Internally, this façade class would handle all the intricate details of coordinating the subsystems.
- **Legacy System Integration**: Suppose you're tasked with integrating a legacy CRM (Customer Relationship Management) system into a modern web application. The legacy system might have a convoluted API with numerous endpoints and data formats. To shield the client code from this complexity and to provide a more straightforward interface, you can create a CRMFacade that encapsulates the interactions with the legacy system. This façade would expose methods such as createCustomer(), updateCustomerInfo(), or getCustomerOrders().
- **Library Interface Simplification**: Consider a scenario where you're developing a software library that wraps around several external libraries or APIs, each with its own initialization routines, configurations, and usage patterns. Instead of forcing users of your library to understand and manage the intricacies of these dependencies, you can create a façade that encapsulates all the necessary initialization and configuration steps. This way, users can interact with a single, cohesive interface provided by your library without worrying about the underlying complexities.
- **Cross-Platform Development**: In a cross-platform application development scenario where you have to manage different platform-specific code paths (e.g., iOS, Android, web), you can employ the Façade pattern to abstract away the platform-specific differences. The façade can provide a unified interface for common tasks such as user authentication, data synchronization, or push notifications, while internally handling the platform-specific implementations.
- **Testing and Mocking**: Facades can also be useful in testing scenarios. If you have a complex system with multiple dependencies, creating facades for subsets of functionality can simplify unit testing. By mocking or stubbing out the facades, you can isolate the code being tested from its dependencies, making the tests more focused and easier to maintain.

In each of these scenarios, the Façade pattern helps to simplify the usage of complex systems or subsystems by providing a unified and simplified interface. It promotes loose coupling between client code and the underlying implementation, thereby enhancing maintainability, scalability, and ease of use.

**Solution**:

From the above definition of the façade pattern, it gives us a simplified interface for working with a complex subsystem. So the above-stated problem of Rubel can be solved using the façade pattern. Rubel can appoint an assistant (a façade class), which will handle the subpart of this complex system (some less important girlfriends over phone and chat) and give day-to-day updates (a common interface) to Rubel. So the life of Rubel will be easy, right?

We can also use or implement the composite pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/53-facade-uml.png"
    caption="UML of Facade Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in the UML diagram we can see that **Clients** interact with the **Façade** class method only. And the **Façade** class internally manages complex subsystems or other classes, which the client needn't worry about.

**When To Use**:
- Use the Façade pattern when you need to have a limited but straightforward interface to a complex subsystem.
- Use the Façade when you want to structure a subsystem into layers.

**Implementation**:
```java
// Complex subsystems
class BankAccount {
    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }

    public double getBalance() {
        return balance;
    }

    public void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrawal successful. Remaining balance: " + balance);
        } else {
            System.out.println("Insufficient funds.");
        }
    }
}

class ATMSystem {
    private BankAccount bankAccount;

    public ATMSystem() {
        this.bankAccount = new BankAccount(1000); // Initial balance for demonstration
    }

    public void validatePin(int pin) {
        // Dummy method to simulate PIN validation
        System.out.println("PIN validated successfully.");
    }

    public void processWithdrawal(double amount) {
        // Dummy method to simulate withdrawal process
        bankAccount.withdraw(amount);
    }
}

// Facade
class ATMFacade {
    private ATMSystem atmSystem;

    public ATMFacade() {
        this.atmSystem = new ATMSystem();
    }

    public void withdrawMoney(int pin, double amount) {
        atmSystem.validatePin(pin);
        atmSystem.processWithdrawal(amount);
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        // Using facade to withdraw money from ATM
        ATMFacade atmFacade = new ATMFacade();
        int pin = 1234; // Dummy PIN for demonstration
        double amount = 200;

        atmFacade.withdrawMoney(pin, amount);
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Structural%20Design%20Pattern/FacadeDesignPattern/C%23).

---

## Achieved Design Principles:
- **Encapsulation**: Façade promotes encapsulation by hiding the complexities of a subsystem behind a single, simplified interface. This allows clients to interact with the system without needing to understand its internal workings, thereby reducing dependencies and coupling.
- **Abstraction**: A façade provides a level of abstraction by presenting a higher-level interface that conceals the details of individual components or subsystems. This abstraction simplifies the interaction for clients and shields them from unnecessary complexity.
- **Simplicity**: A façade simplifies the usage of a complex system by offering a concise and intuitive interface. Clients only need to interact with the facade's methods, rather than dealing with the intricacies of the underlying subsystems, leading to more straightforward code and reduced cognitive load.
- **Modularity**: A façade encourages modularity by breaking down a complex system into smaller, more manageable components. Each subsystem can be encapsulated within its own module, and the façade acts as a coordinator that orchestrates interactions between these modules. This modular structure enhances maintainability and facilitates future changes or updates.
- **Loose Coupling**: Façade promotes loose coupling between client code and the subsystems it interacts with. By providing a well-defined interface, the façade decouples clients from the internal implementation details of the subsystems. This reduces the risk of ripple effects caused by changes to the subsystems and improves the overall flexibility of the system.
- **Single Responsibility Principle (SRP)**: Façade adheres to the SRP by defining a separate class responsible for providing a simplified interface to a subsystem. Each façade class has a clear and focused responsibility, which is to coordinate interactions with the underlying subsystems. This separation of concerns enhances code clarity and maintainability.
- **Simple Interface for Ease of Use**: Façade enhances the usability of a system by providing a user-friendly interface that shields clients from unnecessary complexity. Developers can interact with the facade's methods without needing to understand the intricacies of the underlying subsystems, making it easier to learn, use, and integrate into their applications.