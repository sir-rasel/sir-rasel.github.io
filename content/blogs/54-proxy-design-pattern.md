---
title: "Software Design Patterns and Principles - Part 11 (Proxy Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-14T03:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "proxy-design-pattern"]
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
    image: "img/blogs/54-proxy.png"
    caption: "Proxy Design Pattern"
    alt: "Proxy Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 10:** [Software Design Patterns and Principles - Part 10 (Facade Design Pattern)]({{< ref "blogs/53-facade-design-pattern.md" >}})
- **Part 12:** [Software Design Patterns and Principles - Part 12 (Command Design Pattern)]({{< ref "blogs/55-command-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/54-proxy.png"
    caption="Proxy Design Pattern (Photo Credit: Level Up Coding)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the proxy design pattern.

So let's get started...

---

## Story
Samiul and Ruhul are two close friends. Samiul looks handsome and dashing. On the other hand, Ruhul looks black and fatty. But Ruhul has an online girlfriend. He is very romantic; they chat every day. They have a very good relationship online. But one day the girl wants to meet face-to-face. In this scenario, Ruhul is in very deep tension because he doesn't have enough confidence due to his look. So he decided to send his close and dashing friend Samiul as his proxy.

## Facade Design Pattern
**Definition**:
> Proxy is a structural design pattern that lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

As the definition states, the proxy design pattern suggests a middlemanapproach. It means introducing a substitute for the real one and doing some sanity checks and functionality before the real one and much more. The main goal is to reduce the load and secure the main/original object.

**Problem**:

In the above story, Ruhul doesn't want to meet directly due to his lack of confidence and looks. But he wants to maintain the indirect (online) relationship. So how can he overcome the meeting day without his direct interaction?

The proxy design pattern is versatile and can be applied in various scenarios to address different concerns. Here are some common scenarios where the proxy design pattern can be used:

1. **Virtual Proxy**
> **Scenario**: Loading heavy resources.

**Example**: Imagine an image gallery where high-resolution images are loaded only when they are viewed. A virtual proxy can be used to represent the high-resolution image, loading it only when the user requests to view it.

2. **Protection Proxy**
> **Scenario**: Controlling access to sensitive functionality or data.

**Example**: In a system where certain users have administrative privileges, a protection proxy can restrict access to certain features or data, ensuring that only authorized users can perform certain actions.

3. **Remote Proxy**
> **Scenario**: Accessing objects or services over a network. 

**Example**: When working with distributed systems, a remote proxy can represent an object that resides on a remote server. The proxy handles communication details like network calls, serialization, and deserialization, providing a local representation of the remote object.

4. **Cache Proxy**
> **Scenario**: Caching expensive resource accesses. 

**Example**: Consider a web page that fetches data from a remote server. A cache proxy can store the results of expensive queries or network calls, preventing redundant requests by returning the cached data if the same request is made again.

5. **Logging Proxy**
> **Scenario**: Logging method calls or interactions. 

**Example**: When debugging or monitoring an application, a logging proxy can wrap around an object or service, capturing information about method calls, input parameters, and results. This can be useful for performance monitoring, auditing, or debugging.

6. **Smart Proxy**
> **Scenario**: Adding additional behavior or controlling resource allocation.

**Example**: Imagine a scenario where you want to limit the number of instances of a resource-heavy object in the system. A smart proxy can manage the instantiation of these objects, ensuring that only a certain number are created or that they are created on-demand.

7. **Subject/Observer Proxy**
> **Scenario**: Implementing the observer pattern. 

**Example**: In a system where multiple components need to be notified of changes in another component, a subject/observer proxy can manage the subscription and notification process. Components can subscribe to the proxy, and it can broadcast changes to all subscribers.

8. **Immutable Proxy**
> **Scenario**: Ensuring immutability of objects. 

**Example**: If you want to ensure that certain objects cannot be modified after creation, an immutable proxy can wrap around the original object, preventing any modifications. This is particularly useful in scenarios where data integrity and consistency are critical.

These scenarios highlight the flexibility and usefulness of the proxy design pattern in solving different problems across various domains in software development.

**Solution**:

From the above definition of the proxy pattern, it gives us a middlemancapability. So in the above story, Ruhul sends/sets Samiul as a proxy/middleman, and the issue is solved, right?

We can also use or implement the proxy pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/54-proxy-uml.png"
    caption="UML of Proxy Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in the UML diagram we can see that **Clients** interact with the common interface called **Subject**. And **Proxy** and **RealSubject** implement this common interface. Now when a client calls for **DoAction**() instead of direct access of RealSubject, it first lands on Proxy and then delegates to the real one.

**When To Use**:
- Lazy initialization (virtual proxy). This is when you have a heavyweight service object that wastes system resources by always being up, even though you only need it from time to time.
- Access control (protection proxy). This is when you want only specific clients to be able to use the service object; for instance, when your objects are crucial parts of an operating system and clients are various launched applications (including malicious ones).
- Local execution of a remote service (remote proxy). This is when the service object is located on a remote server.
- Logging requests (logging proxy). This is when you want to keep a history of requests to the service object.
- Caching request results (caching proxy). This is when you need to cache results of client requests and manage the life cycle of this cache, especially if results are quite large.
- Smart reference. This is when you need to be able to dismiss a heavyweight object once there are no clients that use it, etc.

**Implementation**:
```java
// Subject interface
interface Subject {
    void request();
}

// RealSubject class
class RealSubject implements Subject {
    public void request() {
        System.out.println("RealSubject: Handling request.");
    }
}

// Proxy class
class Proxy implements Subject {
    private RealSubject realSubject;

    public void request() {
        // Lazy initialization: create the real subject only when necessary
        if (realSubject == null) {
            realSubject = new RealSubject();
        }
        realSubject.request();
    }
}

// Client class
public class Client {
    public static void main(String[] args) {
        System.out.println("Client: Executing the client code with a real subject:");
        RealSubject realSubject = new RealSubject();
        realSubject.request();

        System.out.println("\nClient: Executing the same client code with a proxy:");
        Proxy proxy = new Proxy();
        proxy.request();
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Structural%20Design%20Pattern/ProxyDesignPattern/C%23).

---

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: The Proxy pattern promotes the separation of concerns by introducing a surrogate object to control access to the real object. This allows each component to focus on a single responsibility: the proxy manages access, while the real object performs its core functionality.
- **Open/Closed Principle (OCP)**: The Proxy pattern allows for the extension of behavior without modifying the underlying code of the real object. New proxy implementations can be introduced to add additional functionality or behavior without altering the original object's code, thus adhering to the OCP.
- **Interface Segregation Principle (ISP)**: By defining a common interface for both the proxy and the real object, the Proxy pattern ensures that clients interact with the proxy in the same way they would with the real object. This promotes a clear and concise interface, adhering to the ISP.
- **Dependency Inversion Principle (DIP)**: Clients depend on the abstract interface provided by the proxy, rather than directly depending on the concrete implementation of the real object. This promotes loose coupling between clients and the real object, facilitating easier maintenance and extensibility, in alignment with the DIP.
- **Encapsulation**: The Proxy pattern encapsulates the access to the real object within the proxy, hiding the complexity of accessing or instantiating the real object from clients. This encapsulation promotes information hiding and protects the real object from unauthorized access or misuse.
- **Reduced Coupling**: The Proxy pattern reduces the coupling between clients and the real object by introducing an intermediary (the proxy) to manage interactions. Clients interact with the proxy, which can handle additional concerns such as lazy initialization, caching, or access control, without the client needing to be aware of these details.
- **Lazy Initialization**: Proxies can employ lazy initialization strategies to defer the creation or loading of the real object until it is actually needed. This promotes efficient resource utilization and improves system performance by only initializing objects when necessary.
- **Performance Optimization**: By introducing proxies to manage access to resources, the Proxy pattern enables performance optimizations such as caching, which can reduce the overhead of repeated access to the same resource. This improves system efficiency and responsiveness.