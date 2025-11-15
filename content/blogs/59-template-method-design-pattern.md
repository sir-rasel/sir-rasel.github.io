---
title: "Software Design Patterns and Principles - Part 16 (Template Method Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-15T10:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "template-method-design-pattern"]
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
    image: "img/blogs/59-template-method.png"
    caption: "Template Method Design Pattern"
    alt: "Template Method Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 15:** [Software Design Patterns and Principles - Part 15 (Strategy Design Pattern)]({{< ref "blogs/58-strategy-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/59-template-method.png"
    caption="Template Method Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the template method design pattern.

So let's get started...

---

## Story
Ripon is known as a love guru who is helping people by advising how they can succeed in their relationship. He shares tips and tricks that can be followed for success in love. Recently he wrote a book called "Success Love," where he shares common guidelines, tips, and tricks for high-value, highly connective relationships. But as people in this world like different things, people are different by their thoughts and by their nature, so how can a common guideline fulfill everyone's hope?

## Template Method Design Pattern
**Definition**:
> The template method is a behavioral design pattern that defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.

As the definition states, it often happens in our program that most of the parts of multiple classes are the same but have a slight difference based on each criterion. So code duplication happens, and the DRY principle breaks. The template method pattern solves this by encapsulating all operations or common codes together in a superclass and offering its subclass to override the particular steps that can vary based on their criteria.

**Problem**:

In the above story, the common guideline against the variation of people's choices, likes, dislikes, and nature is a problem. One solution does not fit all. So how can that be solved, and will the book written by Ripon be a success?

The Template Method design pattern is useful in various scenarios where you have a common algorithm structure but different implementations for certain steps. Here are some scenarios where the Template Method pattern can be applied effectively:
- **Web Application Frameworks**: In web frameworks, you might have a common structure for processing requests (e.g., handling authentication, routing, and response generation), but the specifics of each step can vary based on the type of request or the endpoint being accessed. The Template Method pattern can be used to define the overall request processing flow while allowing subclasses to implement the details for each step.
- **Document Processing**: When working with document processing libraries, such as PDF generation or report generation, you often have a common structure for creating documents (e.g., opening, formatting, adding content, and closing). However, the specifics of content generation or formatting might vary based on the type of document being created. The Template Method pattern can be used to define the document generation algorithm while allowing subclasses to customize the content or formatting.
- **Game Development**: In game development, you might have a common structure for game levels or character behaviors (e.g., initialization, updating game state, rendering, and handling input). However, the specific behavior or appearance of each level or character can vary. The Template Method pattern can be used to define the overall game loop or character behavior while allowing subclasses to implement the details for each level or character.
- **Database Access**: In database access libraries or frameworks, you might have a common structure for executing database queries (e.g., connecting to the database, executing the query, processing the results, and closing the connection). However, the specifics of each query or the type of database being used can vary. The Template Method pattern can be used to define the overall query execution process while allowing subclasses to customize the query construction or result processing.
- **GUI Frameworks**: GUI frameworks often have a common structure for handling user interactions (e.g., initializing components, registering event handlers, processing user input, and updating the display). However, the specifics of each component or interaction might vary. The Template Method pattern can be used to define the overall UI component lifecycle while allowing subclasses to customize the behavior or appearance of each component.
- **Cooking Recipes**: Cooking recipes can be seen as a real-world example of the Template Method pattern. A recipe defines a series of steps (e.g., preparation, cooking, and serving), but the specific ingredients or cooking techniques might vary based on the dish being prepared. The recipe serves as a template method, while the cook can customize each step based on their preferences or available ingredients.

In all these scenarios, the Template Method pattern provides a flexible and reusable way to define the overall structure of an algorithm while allowing subclasses to provide specific implementations for certain steps. This promotes code reuse, encapsulation, and separation of concerns.

**Solution**:

In the above story, Ripon is a very clever boy, and he can assume the problem; that's why, rather than giving a starting guideline, he proposes a template. Also in this template he mentions some points that can vary from person to person, so readers should handle these scenarios by themselves in a personal manner. So the template method design pattern is the rescuer.

We can also use or implement the observer pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/59-template-method-uml.png"
    caption="UML of Template Method Design Pattern (Photo Credit: Medium)"
    align=center
>}}

Here in the UML diagram we can see that an **AbstractTemplateClass** defines and declares all the method signatures and implements them. Also, it declares some methods as **abstract**, as they can be overridden in the **ConcreteClass**. So ConcreteClass overrides the abstract methods based on their need, and the **template method** remains the same, as its functionality is the same for all.

**When To Use**:
- Use the Template Method pattern when you want to let clients extend only particular steps of an algorithm, but not the whole algorithm or its structure.
- Use the pattern when you have several classes that contain almost identical algorithms with some minor differences. As a result, you might need to modify all classes when the algorithm changes.

**Implementation**:
```java
abstract class Game {
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();

    // Template method
    public final void play() {
        // Initialize the game
        initialize();

        // Start the game
        startPlay();

        // End the game
        endPlay();
    }
}

class Cricket extends Game {
    @Override
    void initialize() {
        System.out.println("Cricket Game Initialized! Start playing.");
    }

    @Override
    void startPlay() {
        System.out.println("Cricket Game Started. Enjoy the game!");
    }

    @Override
    void endPlay() {
        System.out.println("Cricket Game Finished!");
    }
}

class Football extends Game {
    @Override
    void initialize() {
        System.out.println("Football Game Initialized! Start playing.");
    }

    @Override
    void startPlay() {
        System.out.println("Football Game Started. Enjoy the game!");
    }

    @Override
    void endPlay() {
        System.out.println("Football Game Finished!");
    }
}

public class TemplateMethodPatternDemo {
    public static void main(String[] args) {
        Game cricket = new Cricket();
        cricket.play();

        System.out.println();

        Game football = new Football();
        football.play();
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Behavioral%20Design%20Pattern/TemplateMethodDesignPattern/C%23).

---

## Achieved Design Principles:
- **Encapsulation**: The Template Method pattern encapsulates the algorithm in a method, providing a clear interface for clients to use. Subclasses can't change the overall algorithm's structure but can modify certain steps.
- **Abstraction**: The pattern allows the abstraction of the overall algorithm while providing concrete implementations for individual steps. This separation of concerns helps in managing complexity.
- **Inheritance**: Template Method relies on inheritance to allow subclasses to provide specific implementations for certain steps of the algorithm. This demonstrates the use of inheritance in OOP.
- **Polymorphism**: Subclasses can provide different implementations for the steps defined in the template method. This demonstrates polymorphism, where different subclasses can be treated interchangeably based on a common interface.
- **Open/Closed Principle (OCP)**: The Template Method pattern follows the OCP by allowing the algorithm's structure to remain unchanged while enabling extension through subclassing. The base template method is closed for modification but open for extension by subclasses.
- **Single Responsibility Principle (SRP)**: The pattern promotes the separation of concerns by allowing subclasses to focus on implementing specific steps of the algorithm. Each subclass is responsible for providing its implementation, adhering to the SRP.
- **Liskov Substitution Principle (LSP)**: Subclasses of the Template Method pattern must be substitutable for their base class. This means that wherever the base class is used, a subclass can be used without affecting the correctness of the program.
- **Dependency Inversion Principle (DIP)**: The Template Method pattern adheres to the DIP by allowing high-level modules to depend on abstractions (i.e., the template method) rather than concrete implementations. Subclasses provide the concrete implementations, promoting flexibility and reusability.