---
title: "Reactive Programming in Java - Part 2 (Thinking In Reactive Way and Reactive Operator)"
description: "Let's learn reactive programming with Java"
date: 2025-10-12
tags: ["programming", "language", "java", "crash-course", "reactive-programming"]
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
    image: "img/blogs/36-reactive-programming.jpeg"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Reactive Programming in Java - Part 1 (Intro)]({{< ref "blogs/35-java-reactive-programming-part-1-intro.md" >}})
- **Part 3:** [Reactive Programming in Java - Part 3 (Introduction of Project Reactor and Some Frequently Used Operators)]({{< ref "blogs/37-java-reactive-programming-part-3-reactor.md" >}})
---

{{< figure
    src="/img/blogs/36-reactive-programming.jpeg"
    caption="Reactive Programming (Photo Credit: zibtek.com)"
    align=center
>}}

In the previous part we were trying to understand what actually reactive programming is and how its mechanism operates. In this part we will try to explore what a reactive operator means and how it works, and gradually we will try to start thinking in a reactive way. So, let's start...

---

## Possible Way of Achieving Non-blocking in Java
As I mentioned in an earlier part, the fundamental agenda of reactive programming is achieving non-blocking and speeding up the application performance. So the asynchronous paradigm is the way. In Java we can achieve asynchronous in some ways. Like:

1. **Callbacks:**
As async methods do not have a return value, we can use a callback function for doing something on finishing the async method. But here the problem is when we need to do multiple and nested async works based on multiple stats, then too many callback functions will be introduced. And as a result, the famous problem will appear: "Callback Hell."
{{< figure
    src="/img/blogs/36-callback-hell.png"
    caption="Callback Hell (Photo Credit: FreeCodeCamp)"
    align=center
>}}

2. **Futures:**
Another way of achieving asynchronous in Java is **Future** and from the **CompletableFuture** class. But the problem with the futures object is that they do not do well at composition, do not support lazy computation, and most importantly, lack support for multiple values and advanced error handling.

The above-mentioned 2 ways are both imperative approaches. To solve the problems, reactive programming paradigms come to the rescue.

## From Imperative to Reactive Programming
Reactive libraries, such as **Reactor**, aim to address these drawbacks of “classic” asynchronous approaches on the JVM while also focusing on a few additional aspects:
- Composability and readability
- Data as a flow manipulated with a rich vocabulary of operators
- Nothing happens until you subscribe
- Backpressure or the ability for the consumer to signal the producer that the rate of emission is too high
- High level but high value abstraction that is concurrency agnostic.

## Initial Steps of Thinking in Reactive Ways
1. The first step and most important thinking should be that **"nothing will happen until you subscribe or observe."** As we already know, reactive programming works in an async way, and it follows the pub/sub or observer/observable pattern, so nothing will be happening before subscription. As a result, we must think in terms of the pub/sub mechanism.
2. Understanding the flow of your application: Is there a need for a blocking call? If so, use a blocking-supported operator. Is there any need to handle exceptions? Is there any need to work with exceptions? Is there any need to convert the input stream type as output or not? How can we break down and think about our application solution in a functional manner, etc.?

The answer to these questions helps us to choose the right type of operators. We will see the operators' details and their example in the upcoming parts, insha Allah. And hopefully, through the deep understanding of operators and using hands-on experience, we will grow our reactive thinking capability gradually. 

So let's see what does **Operator** mean.

## Operator
As we already know from our previous part, reactive programming follows the functional programming style. So, in reactive programming we can consider an operator as a **function**. Operator is a function that, for every element the source Observable emits, applies that function to that item and then emits the resulting element in another Observable.

So, operators operate on an **Observable** and return another Observable. This way, operators can be combined one after the other in a chain to create data flow operations on the events. Each operator adds behavior to a **Publisher** and wraps the previous step’s Publisher into a new instance. The whole chain is thus linked, such that data originates from the first publisher and moves down the chain, transformed by each link. Eventually, a subscriber finishes the process.

## Marble Diagram of Operator Behaviors
The below images show the marble diagrams of operator behaviors. It means different types of operators, how they act with the input data streams, and what type of output stream they generate. It is very important to understand the meaning of each symbol of this diagram because without understanding the meaning of all symbols, it tends to be impossible to understand the documentation of the operator. Please check the images closely and read the description; they are self-explanatory.
{{< figure
    src="/img/blogs/36-reactor-marble-diagram.jpeg"
    caption="Source: Project Reactor"
    align=center
>}}
{{< figure
    src="/img/blogs/36-reactor-marble-diagram-1.jpeg"
    caption="Source: Project Reactor"
    align=center
>}}
{{< figure
    src="/img/blogs/36-marble-diagram.jpeg"
    caption="Source: reactivex.io"
    align=center
>}}

**Behaviors:**
- Most of the operators' input and output event streams are the same, but some operators can change and output different types than input.
- Not all the operators handle error and throw errors on exceptions.
- Most of the operators are non-blocking, and some operators are designed as blocking for using needed cases.
- Some operators are especially designed for handling errors.

### Use Cases Where Reactive Approach Can Be Suitable:
- Highly Concurrent Systems
- Real-time Data Streaming
- Web APIs and Microservices
- User Interfaces (UIs)
- Asynchronous Operations
- Fault Tolerance and Resilience
- Event-driven Architectures
- Reactive Data Processing
- IoT Applications
- WebSockets and Server-Sent Event
- Combining Multiple Data Sources
- Resource Management

### Use Cases Were Reactive Approach Can Be Terrible or Over Killed
- Simple, Synchronous Tasks and Sequential Workflows
- Small, Single-threaded Applications
- Applications with Low Latency Requirements
- Short-lived and CPU-bound Tasks
- Existing Codebase Incompatibility and Legacy Systems
- Limited Development Resources like inexperience reactive developer
- Resource-Intensive Applications
- Strict Real-Time Requirements

### When Choose Reactive Programming Over Traditional One?
- Has Asynchronous and Event-Driven Requirements
- Need Concurrency and Scalability
- Need Responsive User Interfaces
- Need Complex Data Transformation:
- For Real-Time Analytics and Monitoring
- Microservices and Distributed Systems
- Need to handle WebSockets and Server-Sent Events
- Has Complex Event/Stream Processing

---

*Insha Allah, in the upcoming part, I will try to introduce with the project reactor. Until than, may Allah keep you healthy and happy.*