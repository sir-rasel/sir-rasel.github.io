---
title: "Reactive Programming in Java - Part 1 (Intro)"
description: "Let's learn reactive programming with Java"
date: 2025-10-11
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
    image: "img/blogs/35-java-reactive-programming.jpg"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

{{< figure
    src="/img/blogs/35-java-reactive-programming.jpg"
    caption="Reactive Programming (Photo Credit: Reactive Programming Book by Sergi Mansilla)"
    align=center
>}}

Before deep dive into hands on reactive programming using Java, let's understand the core concepts first.

---

## What is Reactive Programming?
In simple words, as its name suggests, reactive programming is a kind of programming paradigm that can react based on something. It uses declarative code (in a manner that is similar to functional programming) in order to build asynchronous processing pipelines. It is an event-based model where data is pushed to the consumer as it becomes available: we deal with asynchronous sequences of events. So reactive programming is programming with asynchronous data streams.

More technically, *"reactive programming is a programming paradigm for asynchronous stream processing with **non-blocking backpressure**."* A **stream** can be best described as a sequence of ongoing events ordered in time.

For understanding reactive programming, it's very important to understand the 2 words, ***"non-blocking"*** and ***"backpressure."***

## What Does Non-blocking Mean?
In our traditional programming, we code in blocking style. That means we code in a manner that every instruction will execute line by line and one after another. And the next line will be executed only when its previous one finishes executing. Similarly, when we work with large data, then we are waiting for the data processing to finish, which is blocking our system and time-consuming as well.

To solve this problem, non-blocking style programming was introduced, which is asynchronous and doesn't block the program execution. Non-blocking programming is a technique used to improve the responsiveness of an application by allowing it to perform multiple I/O operations simultaneously without blocking. In non-blocking programming, the application doesn’t wait for the completion of a task before moving on to the next task. Instead, it checks the status of each task periodically and only acts on completed tasks.

## What Does Backpressure Mean?
In reactive streams, when a reactive application (consumer) is consuming data from the producer, the producer will publish data to the application continuously as a stream. Sometimes the application cannot process the data at the speed of the producer. In this case, the consumer can notify the producer to slow down the data publishing. That means the publisher continuously pushes events/data to the subscriber, but the subscriber can control the events/data load based on its own capability.

{{< figure
    src="/img/blogs/35-backpressure.png"
    caption="Backpressure Controlling (Photo Credit: Project Reactor)"
    align=center
>}}

---

## Characteristics of Reactive System
According to the [reactive-manifesto](https://www.reactivemanifesto.org/), a reactive system has the following characteristics.
- **Responsive:** A reactive system should provide a rapid and consistent response time, and thus a consistent quality of service.
- **Resilient:** A reactive system should remain responsive in case of random failures through replication and isolation.
- **Elastic:** Such a system should remain responsive under unpredictable workloads through cost-effective scalability.
- **Message-Driven:** It should rely on asynchronous message passing between system components.

{{< figure
    src="/img/blogs/35-reactive-manifesto.png"
    caption="Source: Reactive Manifesto"
    align=center
>}}

## High Level Architecture Reactive Programming Follow
We can consider the architecture or flow control mechanism of reactive programming with the **Observable** design pattern. Also, it can be compared with the **Pub-Sub** architecture or **push-based** operation. 

Because in reactive programming, there must be: 
- a publisher, 
- a subscriber, 
- a subscription, and 
- a processor.

{{< figure
    src="/img/blogs/35-observable-pattern.png"
    caption="Observable Design Pattern"
    align=center
>}}

So a subscriber does a subscription to a publisher. Then the publisher publishes data to the processor for processing, and finally the processor pushes the data to the subscriber. That way, without any blocking, the system asynchronously performs its task.

---

## Advantages of Reactive Programming
1. **Efficient resource utilization:** Uses fewer threads by avoiding blocking operations, improving scalability.
2. **Responsive systems:** Enables applications to stay responsive under high load or latency.
3. **Better error handling:** Built-in mechanisms to handle errors gracefully across async data flows.
4. **Real-time updates:** Automatically reflects changes across the system, ideal for real-time applications.
5. **Composable operations:** Makes complex async logic easier to manage using streams and operators.
6. **Improved scalability:** Handles many concurrent tasks efficiently with non-blocking I/O.

## Disadvantages of Reactive Programming
1. **Steep learning curve:** Concepts like streams, backpressure, and observables can be hard to grasp.
2. **Complex debugging:** Tracing issues in asynchronous flows can be more challenging than in imperative code.
3. **Overhead for simple use cases:** Might be overkill for small or straightforward applications.
4. **Limited library support:** Not all libraries or APIs are designed for non-blocking/reactive use.
5. **Harder testing:** Testing asynchronous and time-based logic requires extra tooling and effort.
6. **Increased cognitive load:** Developers must think differently about control flow, state, and timing.

### Available Reactive Programming Library
- For java: **RxJava, Spring WebFlux, Project Reactor**
- For JavaScript: **RxJs**
- For .NET: **Rx.Net**

---

*Insha Allah, in the upcoming part, I will try to share the reactor operators and how to think in reactive way. Until than, may Allah keep you healthy and happy.*