---
title: "Let's Feel Programming Fundamentals - Part 8 (Threads, Asynchronicity, Concurrency, Parallelism)"
description: "You will be a superstar once you begin to feel programming"
date: 2025-08-14
tags: ["programming", "programming-basic", "programming-fundamentals", "threads", "asynchronicity", "concurrency", "parallelism"]
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
    image: "img/blogs/8-concurrency-parallel.jpg"
    caption: "programming"
    alt: "programming"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 7:** [Let's Feel Programming Fundamentals - Part 7 (Algorithm)]({{< ref "blogs/7-lets-feel-programming-part-7-algorithm.md" >}})
---

{{< figure
    src="/img/blogs/8-concurrency-parallel.jpg"
    caption="Concurrency Vs Parallel (Photo Credit: TechDifferences)"
    align=center
>}}

## Story
Remember the principle Virus (Viru Sastre Buddeh) from the 3 Idiots movie. He was able to write simultaneously with his 2 hands. He could do multiple tasks at a time. 

My friend Sharif is a true die-hard fan of Principle Virus. He also can do multiple tasks at a time. He can write with his 2 hands, 2 legs, and other works simultaneously. Sometimes some works depend on each other, and then he has to wait until the dependent work is done. 

For example, when he solves some math equation, he can start writing different equation solutions with his hands and legs, but when one equation result depends on another, he needs to wait until the dependency equation solution. So in a situation like this he waits, and after the result is found, he solves/does other work.

## Asynchronicity (Asynchronous Programming)
According to the MDN web docs ***“Asynchronous programming is a technique that enables your program to start a potentially long-running task and still be able to be responsive to other events while that task runs, rather than having to wait until that task has finished. Once that task has finished, your program is presented with the result.”***

That means it is a technique that is used to optimize our program run time by doing our task simultaneously side by side at a time. So 2 individually independent tasks can be done together side by side with the help of threads.

In the above story Sharif’s multi tasking using 2 hands and legs is an example of asynchronicity. Here his hands and legs are examples of threads and his multiple works done at a time is an example of asynchronous programming.

One important point to be noted is that, we can maximize our uses of asynchronous principle only when our tasks are independent. When they are dependent, like solving the equation, those are mutually dependent then we need to wait which is called the await technique in programming.

## Threads
According to Wikipedia ***“A thread is a small set of instructions designed to be scheduled and executed by the CPU independently of the parent process.”***. So, a thread is the smallest unit of execution in a process. A process can have one or more threads.

That means a unit of work part of the parent process that can be done flawlessly in a CPU memory apart from the parent process or work. 

Like the hands and legs of the above story can be considered a different thread that is part of the parent thread means body.

Other analogy can be, If a process is a kitchen, each thread is a cook. One cook (thread) can do one task at a time; multiple cooks (threads) can prepare multiple dishes simultaneously.

## Concurrency
Simply described, it’s when you are doing more than one thing at the same time. Not to be confused with parallelism, concurrency is when multiple sequences of operations are run in ***overlapping*** periods of time. Means cincurrency is the ability of a system to handle multiple tasks by switching between them (not necessarily at the same time).

Concurrency can be achieved by context-switching for a single core environment and by parallelism for a multi core environment.

Like above, an analogy can be like: one cook juggling several dishes, moving between them quickly.

## Parallelism
Parallelism is more powerful then concurrency. Because it actually running multiple tasks at the ***same time*** — truly simultaneous. So to achieve true parallelism, it requires, multiple CPU cores or multiple machines.

So analogy can be like: several cooks working in the kitchen at the ***same time***, each preparing a dish simultaneously.

---

### Concurrency Vs Parallelism
{{< figure
    src="/img/blogs/8-sequesntial-concurrenct-parallel.webp"
    caption="Sequential vs Concurrent vs Parallel (Photo Credit: Medium)"
    align=center
>}}

| Aspect | Concurrency | Parallelism |
|--------|-------------|-------------|
| **Definition** | Managing multiple tasks at once (interleaved) | Executing multiple tasks at the exact same time |
| **Key Idea** | Task switching | Simultaneous execution |
| **Purpose** | Better responsiveness and resource usage | Faster execution through actual simultaneous work |
| **Hardware** | Can be achieved on a single-core CPU | Requires multi-core CPU or multiple processors |
| **Example** | A single thread switching between tasks | Multiple threads or processes running in parallel |
| **Use Case** | I/O-bound programs (e.g. web servers) | CPU-bound tasks (e.g. video processing, simulations) |
| **Analogy** | One cook handling several dishes by switching | Multiple cooks preparing dishes at the same time |
| **Tools** | Async/await, coroutines, event loops | Multi-threading, multiprocessing |

{{< figure
    src="/img/blogs/8-concurrency-is-not-parallelism.png"
    caption="Concurrency is not Parallelism (Photo Credit: ByteByteGo)"
    align=center
>}}

*“Concurrency is about **dealing** with lots of things at once. Parallelism is about **doing** lots of things at once.”* — Rob Pike

> ⚠️ Note: Parallelism is a subset of concurrency. All parallel programs are concurrent, but not all concurrent programs are parallel.
---
