---
title: "Software Design Patterns and Principles - Part 2 (Classification and Most Used Design Patterns)"
description: "Let's learn the software and oop design patterns and principles!"
date: 2025-10-27
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern"]
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
    image: "img/blogs/44-design-pattern.jpg"
    caption: "Design Patterns and Principles"
    alt: "Design Patterns and Principles"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Software Design Patterns and Principles - Part 1 (Introduction)]({{< ref "blogs/44-design-pattern-principle-intro.md" >}})
- **Part 3:** [Software Design Patterns and Principles - Part 3 (Relations Between Objects and UML Diagram)]({{< ref "blogs/47-objects-relation-and-uml.md" >}})
---

{{< figure
    src="/img/blogs/45-design-pattern.png"
    caption="Design Patterns and Principles (Photo Credit: meduim.com)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the classification of OOP design patterns and list of some of the most used design patterns.

So let's get started...

---

## Story
When we want to do big things, then we need to maintain 3 major points. Like: 
1. Creating its smallest parts
2. Structure them properly
3. Controlling their behaviors

So it's really important to look after all these 3 points for obtaining a maintainable big system. Because unnecessary more things creation than needed, unstructured the smallest parts of the system and not proper controlling their behaviors can easily break the whole system.

## OOP Design Patterns
In short, design patterns provide low-level solutions related to the implementation of commonly occurring object-oriented problems. In other words, the design pattern suggests a specific implementation for the specific object-oriented programming problem.  That design pattern gives us a solution with implementation guidelines for commonly occurring object-oriented problems when we are creating software.

## Classification of Design Patterns
Depending on the problem and solution domains and design patterns, they can be classified into 3 types: They are:


{{< figure
    src="/img/blogs/45-design-pattern-classification.png"
    caption="Design Patterns Classification (Photo Credit: javaScript.plainenglish.io)"
    align=center
>}}

### 1. Creation Design Patterns:
As its name refers, this type of design pattern is concerned about the creation of objects. This means creational design patterns give us an implementational guideline for how objects can be created efficiently and with an extendable procedure. This type of design pattern describes the scenario when and how objects can be created without memory leaks and increases the flexibility and reuse of existing code. Some well-known and most-used creational design patterns are:
- **Singleton** — It describes how we can create only one single instance or object of a class.
- **Factory / Factory method** — It describes how we can create objects through an interface or methods.
- **Abstract factory** — It tells us about the procedure of creating related groups of objects when we need them.
- **Builder** — It helps us construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.
- **Prototype** — This pattern gives us a way to copy existing objects without making your code dependent on their classes.

### 2. Structural Design Patterns:
After creating lots of objects, we need to organize them so that they are lying in a proper structure, and we can reuse, extend, and handle them in a hassle-free manner. Here come the structural design patterns, which explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient. It also ensures that functionalities are properly separated and encapsulated. It reduces the minimal interface between interdependent things. Some well-known and most-used structural design patterns are:
- **Decorator** — It allows us to attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.
- **Adapter** — It allows objects with incompatible interfaces to collaborate.
- **Composite** — It composes objects into tree structures and then works with these structures as if they were individual objects.
- **Facade** — It provides a simplified interface to a library, a framework, or any other complex set of classes.
- **Proxy** — It provides a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

### 3. Behavioral Design Patterns:
As mentioned in the story section, for a successful and well-maintained big system creation, it is not all about things and structuring them; controlling the behaviors is also equally important. Behavioral design patterns perform this vital role. It takes care of effective communication and the assignment of responsibilities between objects. It describes interactions between objects and focuses on how objects communicate with each other. Some well-known and most-used behavioral design patterns are:
- **Strategy** — It defines a family of algorithms, puts each of them into a separate class, and makes their objects interchangeable.
- **Observer** — It defines a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.
- **Mediator** — It reduces chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.
- **Command** — It turns a request into a stand-alone object that contains all information about the request. This transformation lets you pass requests as method arguments, delay or queue a request’s execution, and support undoable operations.
- **Template method** — It defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.