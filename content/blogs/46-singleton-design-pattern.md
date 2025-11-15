---
title: "Software Design Patterns and Principles - Part 4 (Singleton Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: 2025-10-29
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "singleton-design-pattern"]
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
    image: "img/blogs/46-singleton.png"
    caption: "Singleton Design Pattern"
    alt: "Singleton Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 3:** [Software Design Patterns and Principles - Part 3 (Relations Between Objects and UML Diagram)]({{< ref "blogs/47-objects-relation-and-uml.md" >}})
- **Part 5:** [Software Design Patterns and Principles - Part 5 (Factory Method and Abstract Factory Method Design Pattern)]({{< ref "blogs/48-factory-and-abstract-factory-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/46-singleton.png"
    caption="Singleton Design Pattern (Photo Credit: refactoring.guru)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the singleton design pattern.

So let's get started...

---

## Story
Ismael is a very good boy and over 21 years old. As he is an adult now, he decided to marry someone and addressed him as my wife. As I previously stated, he is a good boy (though, like other men, he also has petty thinking), and he desires only one wife in his entire life. So he is looking for a wife until he finds someone to be his wife. When he found someone, he left his entire life with her and refused to accept any other girls as his wife.

Now he is in search of his singleton wife.

## Singleton Design Pattern
{{< figure
    src="/img/blogs/46-singleton-1.png"
    caption="Singleton Design Pattern (Photo Credit: refactoring.guru)"
    align=center
>}}

The singleton design pattern is a creational design pattern that helps us to create and maintain only one instance of a class. That is, as its name refers, the singleton design pattern gives us a way to create only one instance object of a class and ensure the use of this object everywhere in the system. 

Like the Ismael in the above story, he allows the first woman as his wife; after that, he refuses the other instances of women as his wife.

### Problems The Singleton Design Pattern Solves:
We know every design pattern is meant to solve some design problems; the singleton design pattern also solves 2 problems. Like:
1. Ensures that a class has just only one single instance object.
2. Provide a global access point to that instance.

### Singleton Design Pattern Applicability:
- Use the Singleton pattern when a class in your program should have just a single instance available to all clients; for example, a single database object shared by different parts of the program or a logger for log systems' different messages.
- Use the Singleton pattern when you need stricter control over global variables.

### UML Diagram:
{{< figure
    src="/img/blogs/46-singleton-uml.jpg"
    caption="Singleton Design Pattern UML (Photo Credit: tutorialspoint.com)"
    align=center
>}}

You can see in the above UML diagram that every time a caller requests an instance, it returns the already created instance.

## Implementation
***Java:***
```java
package sir.singleton.example.thread_safe;

public final class Wife {

    private static volatile Wife wife;
    public int counter = 0;

    private Wife () {
        this.counter++;
    }

    public static Wife getInstance() {
        Singleton result = wife;
        if (result != null) {
            return result;
        }
        synchronized(Wife.class) {
            if (wife == null) {
                wife = new Wife();
            }
            return wife;
        }
    }
}

// Caller
public class DemoMultiThread {
    public static void main(String[] args) {
        Thread threadFoo = new Thread(new ThreadFoo());
        Thread threadBar = new Thread(new ThreadBar());
        threadFoo.start();
        threadBar.start();
    }

    static class ThreadFoo implements Runnable {
        @Override
        public void run() {
            Wife wife = Wife.getInstance();
            System.out.println(wife.counter);
        }
    }

    static class ThreadBar implements Runnable {
        @Override
        public void run() {
            Wife wife = Wife.getInstance();
            System.out.println(wife.counter);
        }
    }
}
```

***C#:***
```c#
using System;

namespace SingletonDesignPattern
{
    sealed class Wife
    {
        // Step 1: Create a single, readonly instance at class load time
        private static readonly Wife instance = new Wife();

        // Step 2: Track number of instances (should always be 1)
        public static int NumberOfInstance { get; private set; }

        // Step 3: Private constructor prevents external instantiation
        private Wife()
        {
            NumberOfInstance++;
            Console.WriteLine("Wife instance created.");
        }

        // Step 4: Provide a global access point
        public static Wife Instance
        {
            get { return instance; }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Access singleton instance
            Wife wife1 = Wife.Instance;
            Console.WriteLine($"Number of instances: {Wife.NumberOfInstance}");

            // This line would cause a compile-time error because the constructor is private
            // Wife obj = new Wife(); 

            Wife wife2 = Wife.Instance;
            Console.WriteLine($"Number of instances: {Wife.NumberOfInstance}");

            // Confirm both references point to the same instance
            Console.WriteLine($"Are wife1 and wife2 same instance? {ReferenceEquals(wife1, wife2)}");
        }
    }
}
```

The above implementation is fine and simple enough, but here is a problem when we are working on a multithread. Because in the multithread system we can't guarantee 100% that only one instance will be created because more than 1 thread can access the class simultaneously and create multiple instances of the class and break the singleton rule. So we have a thread-safe implementation of the singleton design pattern as below.

```c#
using System;
using System.Threading;

namespace SingletonDesignPattern
{
    class Wife
    {
        private Wife() { }

        private static Wife _instance;
        private static readonly object _lock = new object();

        public static Wife GetInstance(string value)
        {
            if (_instance == null)
            {
                lock (_lock)
                {
                    if (_instance == null)
                    {
                        _instance = new Wife();
                        NumberOfInstance++;
                        Console.WriteLine($"Wife instance created with value: {value}");
                    }
                }
            }
            return _instance;
        }

        public static int NumberOfInstance { get; private set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Thread process1 = new Thread(() =>
            {
                TestSingleton("First");
            });

            Thread process2 = new Thread(() =>
            {
                TestSingleton("Second");
            });

            process1.Start();
            process2.Start();

            process1.Join();
            process2.Join();

            Console.WriteLine($"Total number of Wife instances created: {Wife.NumberOfInstance}");
        }

        static void TestSingleton(string value)
        {
            Wife singleton = Wife.GetInstance(value);
            Console.WriteLine($"Thread {Thread.CurrentThread.ManagedThreadId} got instance hash: {singleton.GetHashCode()}");
        }
    }
}
```

---

### Points To Remember About Singleton:
- Use singleton pattern when your system need only one instance of a class to all its clients.
- Use singleton when you need stricter control over global variables.
- When implementing singleton pattern, multithreaded scenario keeps in mind always.