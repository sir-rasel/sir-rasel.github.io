---
title: "Software Design Patterns and Principles - Part 15 (Strategy Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-15T08:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "strategy-design-pattern"]
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
    image: "img/blogs/58-strategy.jpg"
    caption: "Strategy Design Pattern"
    alt: "Strategy Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 14:** [Software Design Patterns and Principles - Part 14 (Observer Design Pattern)]({{< ref "blogs/57-observer-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/58-strategy.jpg"
    caption="Strategy Design Pattern (Photo Credit: Digital Ocean)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the strategy design pattern.

So let's get started...

---

## Story
Sharif is a cunning person who works as a salesman on a marketing team. His main job is to convince people and sell goods. As we all know, convincing people is a tough task, and different people are convinced in different ways. So Sharif needs to meet many people with different thoughts and observe them closely. After that, he needs to shift or switch his way of convincing based on people's mode and choice. But the ultimate goal is to convince and sell goods.

## Strategy Design Pattern
**Definition**:
> Strategy is a behavioral design pattern that lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.

As the definition states, the strategy pattern gives a way of runtime algorithm change of some processing mechanism or so-called algorithm. Without breaking any code or working procedure, the client just changes the algorithm class, and that's it.

**Problem**:

In the above story, one of the biggest problems of Sharif is handling different types of people. Not everyone is convinced by the same approach. So he needs a different approach. But switching frequently between modes is tough. How can he handle that?

The strategy design pattern is incredibly versatile and can be applied in various scenarios across software development. Here are some common situations where the strategy pattern can be used effectively:
- **Sorting Algorithms**: Different sorting algorithms (such as bubble sort, quick sort, and merge sort) can be encapsulated within separate strategy classes. Depending on the size or characteristics of the dataset, the appropriate sorting strategy can be selected dynamically.
- **Data Validation**: In a system where data validation rules may vary based on user roles or input sources, using the Strategy pattern allows you to encapsulate different validation strategies. For example, one strategy might enforce stricter validation for administrative users, while another might allow more leniency for regular users.
- **File Compression**: When implementing file compression utilities, different compression algorithms (e.g., gzip, zlib, bzip2) can be encapsulated as strategies. Users can then choose the compression strategy based on factors such as file type or desired compression ratio.
- **Authentication and Authorization**: In a system with multiple authentication methods (e.g., username/password, OAuth, JWT), each authentication method can be implemented as a separate strategy. Similarly, different authorization strategies (e.g., role-based access control, attribute-based access control) can be encapsulated using the Strategy pattern.
- **Payment Processing**: In an e-commerce application, various payment gateways (e.g., PayPal, Stripe) can be encapsulated as separate strategies. This allows the system to switch between payment processors seamlessly or even use multiple processors concurrently.
- **Pathfinding Algorithms**: In a game or navigation system, different pathfinding algorithms (e.g., A*, Dijkstra's algorithm, breadth-first search) can be implemented as strategies. The choice of algorithm may depend on factors such as computational resources or desired path optimality.
- **Logging and Error Handling**: Strategies can be used to handle logging and error handling in different ways. For example, one strategy might log errors to a local file, while another might send them to a remote server for monitoring and analysis.
- **Cache Management**: In systems where caching is used to improve performance, different caching strategies (e.g., least recently used, least frequently used, time-based expiration) can be encapsulated as strategies. This allows the system to adapt its caching strategy based on usage patterns or resource constraints.
- **Game AI**: In a game with AI opponents, different strategies can be employed based on the behavior of the player or other game conditions. Each AI strategy, such as aggressive, defensive, or balanced, can be implemented separately and switched dynamically during gameplay.
- **Text Processing**: In a text editor application, you might want to implement different text formatting strategies (e.g., Markdown, HTML, or plain text) for displaying or exporting documents. Users can choose the desired formatting strategy based on their needs.
- **Image Processing**: In an image editing application, various image manipulation algorithms (e.g., resizing, cropping, and filtering) can be implemented as strategies. Users can select the appropriate manipulation strategy depending on the desired effect for their images.

These are just a few examples of how the strategy design pattern can be applied in software development to achieve flexibility, maintainability, and reusability in code.

**Solution**:

In the above story, Sharif can define a different strategy for convincing people of a different type. All the strategy's end goal is convincing. So Sharif can easily switch between these strategies based on the scenario, and the problem is solved.

We can also use or implement the strategy pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/58-strategy-uml.png"
    caption="UML of Strategy Design Pattern (Photo Credit: dotnettricks.com)"
    align=center
>}}

Here in the UML diagram we can see that the **Client** (sometimes also called the **Context**) holds a reference to the **Strategy** interface. And the other **ConcreteStrategy** class implements the same **Strategy** interface. So the **Client** can change the **ConcreteStrategy** at runtime for algorithm changes.

**When To Use**:
- Use the Strategy pattern when you want to use different variants of an algorithm within an object and be able to switch from one algorithm to another during runtime.
- Use the Strategy when you have a lot of similar classes that only differ in the way they execute some behavior.
- Use the pattern to isolate the business logic of a class from the implementation details of algorithms that may not be as important in the context of that logic.
- Use the pattern when your class has a massive conditional statement that switches between different variants of the same algorithm.

**Implementation**:
```java
// Define the strategy interface
interface PaymentStrategy {
    void pay(double amount);
}

// Concrete strategy: Credit Card payment
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    private String expiryDate;
    private String cvv;

    public CreditCardPayment(String cardNumber, String expiryDate, String cvv) {
        this.cardNumber = cardNumber;
        this.expiryDate = expiryDate;
        this.cvv = cvv;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using Credit Card");
        // Additional logic for processing credit card payment
    }
}

// Concrete strategy: PayPal payment
class PayPalPayment implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalPayment(String email, String password) {
        this.email = email;
        this.password = password;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using PayPal");
        // Additional logic for processing PayPal payment
    }
}

// Context class
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(double amount) {
        paymentStrategy.pay(amount);
    }
}

// Client code
public class StrategyPatternExample {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // Customer wants to pay using Credit Card
        cart.setPaymentStrategy(new CreditCardPayment("1234567890123456", "12/25", "123"));
        cart.checkout(100.0);

        // Customer changes payment method to PayPal
        cart.setPaymentStrategy(new PayPalPayment("example@example.com", "password123"));
        cart.checkout(50.0);
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Behavioral%20Design%20Pattern/StrategyDesignPattern/C%23).

---

## Achieved Design Principles:
- **Encapsulation**: Each strategy (or algorithm) is encapsulated within its own class, allowing its implementation details to be hidden from the client code. This promotes encapsulation, a fundamental principle of OOP, by preventing direct access to strategy internals and ensuring that changes to one strategy do not affect others.
- **Abstraction**: The Strategy pattern abstracts the behavior of each algorithm into a common interface or base class. This abstraction allows clients to interact with different strategies using a unified interface, without needing to know the specific details of each strategy's implementation.
- **Inheritance/Polymorphism**: Strategies are typically implemented using inheritance and polymorphism. Each strategy class inherits from a common base class or implements a shared interface, enabling polymorphic behavior. This allows clients to use strategies interchangeably, treating them uniformly based on their common interface.
- **Composition over Inheritance**: The Strategy pattern favors composition over inheritance by allowing algorithms to be composed with client objects. Instead of inheriting behavior directly, clients can hold a reference to a strategy object and delegate behavior to it dynamically. This promotes code reuse and flexibility, as strategies can be easily swapped or extended without modifying client code.
- **Single Responsibility Principle (SRP)**: Each strategy class has a single responsibility: encapsulating a specific algorithm or behavior. This adherence to the SRP promotes code maintainability and modularity, as changes to one strategy are isolated and do not affect other parts of the system.
- **Open/Closed Principle (OCP)**: The Strategy pattern supports the Open/Closed Principle by allowing new strategies to be added without modifying existing client code. Clients depend on abstractions (interfaces or base classes) rather than concrete implementations, making it easy to extend the system with new strategies without altering the existing codebase.
- **Dependency Inversion Principle (DIP)**: The Strategy pattern facilitates the Dependency Inversion Principle by decoupling client code from concrete strategy implementations. Clients depend on abstractions (interfaces or base classes) rather than concrete classes, allowing them to be independent of specific implementations and promoting flexibility and extensibility.