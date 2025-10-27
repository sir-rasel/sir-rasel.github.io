---
title: "Software Design Patterns and Principles - Part 1 (Introduction)"
description: "Let's learn the software and oop design patterns and principles"
date: 2025-10-26
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
- **Part 2:** [Software Design Patterns and Principles - Part 2 (Classification and Most Used Design Patterns)]({{< ref "blogs/45-design-pattern-principle-classification.md" >}})
---

{{< figure
    src="/img/blogs/44-design-pattern.jpg"
    caption="Design Patterns and Principles (Photo Credit: educba.com)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. Before diving into any specific patterns, let's try to understand what software patterns and principles mean.

So let's get started...

---

## Story
Aslam was born into a decent family and lives in an urban area. His father and mother are educated people. As a result, they always try to teach Aslam good things.

Aslam's mother is a principal. She always gives advice and teaches techniques on how Aslam can be better in his work and avoid problems in his work. She told Aslam that if he follows the techniques and his advice, then he can avoid problems in his work, but she never told Aslam how he can solve the well-known problems if they arise.

On the other hand, Aslam’s father is a pattern master. He teaches Aslam how to solve well-known problems in his work if they arise. He teaches the situation of how Aslam can identify the problems and apply the solution when needed.

Now Aslam becomes a very efficient worker in his field by obeying his principled mother's advice and techniques and his pattern-master father's problem identification and applying solution techniques.

So you can easily see that design patterns and design principles are not the same things. There is a clear difference between them. 

## Design Principles
Design principles provide high-level guidelines to design better software applications. They do not provide implementation guidelines and are not bound to any programming language. It means they just give us advice and techniques like Aslam’s mother and don’t give us any implementation details. Design principle tells us how we can keep our design simple, elegant, and efficient by following some advice.

Some well-known design principles are SOLID, DRY, KISS, etc.

## Design Patterns
Design patterns provide low-level solutions related to the implementation of commonly occurring object-oriented problems. In other words, the design pattern suggests a specific implementation for the specific object-oriented programming problem. This means that, like Aslam’s father, design patterns give problem specifications, a solution model, and a solution. It describes what type of problems our software implementation can face and what would be the best solution for it.

Some well-known design patterns are Singleton, Adapter, Mediator, Factory, etc.

---

## Object Oriented Programming (OOP)
OOP is a programming paradigm of wrapping the real-world data. It means packing together the state and behavior of a real-world object. Before understanding the design patterns and principles, everybody must need to know and have a clear understanding of OOP and the pillars of it.

I wrote a short brief about the OOP in my [this]({{< ref "blogs/5-lets-feel-programming-part-5-programming-style.md" >}}) and [this]({{< ref "blogs/32-java-part-3-oop.md" >}}) previous post. Please read this before you continue further reading.

## Software Design (Object-Oriented) Principles
There are some well-known and proven principles in object-oriented programming. Like:
- **Identify the aspects of your application that vary and separate them from what stays the same.**
- **Program to an interface, not an implementation. Depend on abstractions, not on concrete classes.**
- **Favor composition over inheritance.**
- **SOLID principles.**

According to the book *Head First Object-Oriented Analysis & Design (OOAD)*, great software has 3 basic characteristics:
1. **Great software must satisfy the customer's needs.**
2. **Great software is well designed, well coded, reusable, easy to maintain, and extendable.**
3. **Great software is always ready to adopt changes.**

So if we take a deep dive at these characteristics, then it is very clear and understandable that great software is well coded so that it becomes easily maintainable, reusable, and ready to adopt the new changes or requirements by the customers so that it can fulfill the customer needs.

As a result, to make our software great, well, and easily maintained, we need to apply some well-known object-oriented (OO) design principles. These OO principles make our code loosely coupled, extensible, and adaptable to changes.

Let's discuss some of the principles briefly:

### 1. Ideal Encapsulation:
Encapsulate separately what varies and what remains almost unchanged. In that manner you need to maintain only the changing parts of the system based on the change.

Suppose you have a class that has some property and methods that remain almost unchanged; on the other hand, this class also has some property and methods that can vary over time. So please separate the varying parts of the class into a separate object, and that gives you easily adopted power over the changes.

### 2. Interfacing Rather Than Implementing:
Code to an interface rather than to an implementation. This means when you have a bunch of related methods that can vary in their functionality based on situation and algorithms, then please organize them using an interface rather than direct implementation. In that way you get better flexibility.

### 3. Single Reason To Change:
Each class in your application should have only one reason to change. It means your class should be modular enough and specific enough that you need to change it only for a single reason. If your class needs to change frequently and for more than one reason, then you should consider it to be redesigned because it's not well designed.

### 4. Behavior and Functionality:
Classes are about behavior and functionality. This means in object-oriented programming, a class is the blueprint of a single object, including its property, behavior, and functionality. So please make a class where it represents a single object, not more than one specific thing.

### 5. Open-Closed Principle (OCP):
Classes should be open for extension but close for modification. It means when you design your class, design it with perfection, and nobody should modify this perfect class. But if anybody wants to extend it, then they can do it by inheriting the class, and these new classes can add or override the base class functionality according to the requirements.

### 6. Don't Repeat Yourself Principle (DRY):
Avoid duplicate code by abstracting out things that are common and placing them in a single location. It is the most traditional thing to make our code robust and clean. We should always try to identify the common functionality and behavior of our system and place them in a single location so that we can always use them without rewriting again. In that way our code becomes smaller and clean enough and easy to maintain.

### 7. Single Responsibility Principle (SRP):
Every object in your system should have a single responsibility, and all the object’s services should be focused on carrying out that single responsibility. It is similar to our previously mentioned principle, which is that our class should have only one reason to change. So when you ensure the class and services are designed for single responsibility, then automatically it ensures it changes only when this single responsibility-related change occurs.

### 8. Liskov Substitution Principle (LSP):
Subclasses should be substitutable for their base classes. As we know, subclasses can be assigned to base classes. This principle states that we should design our base class and subclasses so that subclasses can be completely substitutable by the base class. In that way we can make a common and parent-responsible class that can handle all its children all together.

---

## Final Words:
Always remember that, if you do it the first time just do it, if you do the same thing second time then start thinking about refactoring and apply OO principles. But if you do it for a third time then definitely start refactoring it by applying all possible OO principles and other stuff.

One last thing: always remember, ***"Most good designs come from the analysis of bad design."*** So analyze your code's current design, apply principles, and make it good.