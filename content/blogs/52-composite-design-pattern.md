---
title: "Software Design Patterns and Principles - Part 9 (Composite Design Pattern)"
description: "Let's learn the software and oop design patterns and principles!"
date: "2025-11-11"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "composite-design-pattern"]
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
- **Part 8:** [Software Design Patterns and Principles - Part 8 (Decorator Design Pattern)]({{< ref "blogs/51-decorator-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/52-composite.png"
    caption="Composite Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the composite design pattern.

So let's get started...

---

## Story
One of my close bros, Siam, wants to create a quiz competition app. The feature of this app will be fantastic. Siam bro wants, in a running quiz competition, both a single individual player and multiple players as a team to participate. So the score will be calculated based on the player's individual points and also his team members' points (if any), and the leadership board will be updated based on that. Now Siam, bro, is in tension about how he will design and develop his code to tackle this complex, composite, hierarchical, and tree-like structure (team players' connection).

## Composite Design Pattern
**Definition**:
> Composite is a structural design pattern that lets you compose objects into tree structures and then work with these structures as if they were individual objects.

As the definition states, the composite pattern helps us to compose and interact with complex, hierarchical, or tree-structured systems. It gives an opportunity to work with a complex and composite object as an individual object. The user or caller needn't be concerned about the structure; they just use the common interface. That's it.

**Problem**:

In the above story, Siam bro faces a problem of maintaining the composition and hierarchical structures of players. Another challenging part is combining the team players and treating them as individual players (as single and team players can both participate). Also, another challenge is calculating the score. So how can Siam Bro design for solving these problems?

Certainly! The composite design pattern is applicable in various scenarios where you have hierarchical/tree structures and need to treat individual objects and compositions of objects uniformly. Below are some scenarios where the composite pattern can be applied:
- **Graphic Design Software**: In graphic design software, you might have shapes (like circles, squares, and triangles) as individual objects, and you might also have composite objects like groups or layers that contain multiple shapes. The composite pattern can be used to represent these structures uniformly, allowing you to perform operations on individual shapes or groups of shapes.
- **File System**: In a file system, directories can contain files and other directories. This hierarchical structure can be modeled using the composite pattern, where directories and files are treated uniformly as components. This allows for operations such as navigating through the file system, copying, moving, or deleting files and directories regardless of their individual or composite nature.
- **Organization Hierarchy**: In an organizational hierarchy, you have individual employees as well as departments, which can contain sub-departments or other employees. Using the composite pattern, you can model the organization's structure uniformly, allowing you to perform operations such as calculating salaries, managing permissions, or analyzing the hierarchy.
- **Menu Systems**: As demonstrated in the bakery story, menu systems can benefit from the composite pattern. Individual menu items like dishes or drinks can be represented as leaf components, while combo meals or meal deals can be represented as composite components. This allows for flexible menu management and customization.
- **GUI Components**: Graphical user interfaces often have complex structures, with components like buttons, checkboxes, and text fields arranged in panels, tabs, or other containers. The composite pattern can be used to represent these structures uniformly, enabling operations such as rendering, event handling, or layout management.
- **Organization of Tasks**: In a task management application, tasks can have subtasks or be grouped into projects. The composite pattern can be used to represent tasks and projects uniformly, allowing for operations such as tracking progress, assigning responsibilities, or scheduling.

In all these scenarios, the composite pattern provides a way to work with hierarchical structures in a consistent and flexible manner, enabling you to treat individual elements and compositions of elements uniformly.

**Solution**:

From the above definition of composite pattern, it gives us a power of composite multiple object and gives a common interface to working with them as if it is an individual object. So in the above stated problem of Siam bro can be solved using the composite pattern. Siam bro can declare a common interface which gives a method of calculating points and both composite object (team, collection of players) and single object (individual player) will implement. That way client can be just call the point calculation method and the overall problem solved.

We can also use or implement composite pattern as a solution of the problems stated earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/52-composite-uml.jpeg"
    caption="UML of Composite Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in UML diagram we can see that, **Client** interacts with **Component** interface. And **Leaf** (which is a standalone object) and **Composite** (which is a complex/combination of **Leaf** objects) implements the **Component** interface. So Client need not know about the objects type (**Leaf** or **Composite**). **Client** can interact like e individual object.

*Type safety* primarily concerns ensuring that the types of components being combined are compatible and safe at compile time, preventing type-related errors. *Uniformity* focuses on providing a consistent interface for interacting with components and composites, promoting simplicity, modularity, and ease of use for clients.

**When To Use**:
- Use the Composite pattern when you have to implement a tree-like object structure.
- Use the pattern when you want the client code to treat both simple and complex elements uniformly.

**Implementation**:
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public interface Score {
    double calculatePoint();
}

public class Player implements Score {
    private final double point;

    public Player(double point) {
        this.point= point;
    }

    @Override
    public double calculatePoint() {
        return point;
    }
}

public class Team implements Score {
    private final List<Player> players = new ArrayList<>();

    public Team(Player... players) {
        children.addAll(Arrays.asList(players));
    }

    @Override
    public double calculatePoint() {
        return players.stream().mapToDouble(Player::calculatePoint).sum();
    }
}

public class QuizApp {

    public static void main(String[] args) {
        Score player1 = new Player(20);

        Score player2 = new Player(10);
        Score player3 = new Player(30);
        Score team1 = new Team(player2, player3);

        System.out.println(player1.calculatePoint());
        System.out.println(team1.calculatePoint());
    }

}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Structural%20Design%20Pattern/CompositeDesignPattern/C%23).

---

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: By abstracting both individual objects and compositions of objects into a common interface, the Composite pattern ensures that each class has a single responsibility: either representing an individual object or managing a collection of objects. This separation of concerns improves the clarity and maintainability of the codebase.
- **Open/Closed Principle (OCP)**: The Composite pattern allows for the addition of new types of components (either individual or composite) without modifying existing code. This is achieved by programming to an interface rather than a concrete implementation, allowing for extension without modification. As a result, the system is open for extension but closed for modification.
- **Liskov Substitution Principle (LSP)**: Components in the Composite pattern adhere to a common interface, ensuring that they can be substituted interchangeably without affecting the correctness of the program. This principle encourages the use of polymorphism, allowing clients to treat individual objects and compositions of objects uniformly.
- **Dependency Inversion Principle (DIP)**: The Composite pattern decouples higher-level modules (clients) from the implementation details of individual components and compositions of components. Clients depend on abstractions (e.g., interfaces) rather than concrete implementations, promoting flexibility and ease of maintenance.
- **Interface Segregation Principle (ISP)**: The common interface used in the Composite pattern is tailored to the needs of clients, ensuring that clients only depend on the methods they require. This prevents clients from being forced to depend on methods that they don't use, promoting a more cohesive and maintainable design.
- **Composition over Inheritance**: The Composite pattern favors composition over inheritance, allowing for flexible and dynamic structures to be built from simple components. This approach promotes code reuse, as components can be combined in various ways to create complex structures without the limitations and complexities of inheritance hierarchies.