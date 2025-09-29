---
title: "Java Crash Course - Part 5 (Thread Programming)"
description: "Let's learn writing program with Java"
date: 2025-09-30
tags: ["programming", "language", "java", "crash-course", "thread-programming"]
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
    image: "img/blogs/34-java-threading.png"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 4:** [Java Crash Course - Part 4 (Miscellaneous)]({{< ref "blogs/33-java-part-4-miscellaneous.md" >}})
---

{{< figure
    src="/img/blogs/34-java-threading.png"
    caption="Java Thread Programming (Photo Credit: Medium)"
    align=center
>}}

***N.B:*** Please read the following concepts for better understanding before continue reading this article.

☛ [Threads, Asynchronicity, Concurrency, Parallelism]({{< ref "blogs/8-lets-feel-programming-part-8-concurrency-parallel.md" >}})

---

### What is a Thread?
- A thread = a lightweight unit of execution within a process.
- A Java process (JVM instance) always starts with main thread.

### What is Multi-Threading?
- Multithreading means executing multiple threads concurrently in a single program. 
- Normally Java programs run on single thread called main thread. 
- But you can create more threads to run tasks concurrently (not necessarily in parallel, depends on CPU cores & scheduling).

👉 Benefit: Run multiple things at once (e.g., UI stays responsive while downloading data).

### Benefits of Multithreading:
- Better CPU utilization
- Faster execution of independent tasks
- Efficient resource sharing
- Makes real-time apps responsive
- Handles multiple tasks simultaneously (like UI + background download)
- Essential for concurrent systems, gaming, real-time applications

### Thread Creation Process
There are several ways to create thread in Java. Some of them are below:

1. Extending Thread:
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Running in: " + Thread.currentThread().getName());
    }
}

public class Demo {
    public static void main(String[] args) {
        Thread t = new MyThread();
        t.start(); // start() creates a new thread and calls run()
    }
}
```

2. Implementing Runnable / Callable:
```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Task executed by: " + Thread.currentThread().getName());
    }
}

public class Demo {
    public static void main(String[] args) {
        Thread t = new Thread(new MyTask());
        t.start();
    }
}
```
> Prefer Runnable if your class needs to extend another class.

3. With Lambda (modern style):
```java
Thread t = new Thread(() -> {
    System.out.println("Running with lambda!");
});
t.start();
```

### Thread Lifecycle
A thread goes through states:

- NEW → after creation (new Thread(...)).
- RUNNABLE → after calling start().
- RUNNING → when CPU picks it.
- WAITING / TIMED_WAITING / BLOCKED → when waiting or locked.
- TERMINATED → after finishing run().

👉 We can inspect state with t.getState().

### Common Java Thread Methods
1. `start()`

Starts a new thread and internally calls `run()`.
```java
new Thread(() -> System.out.println("Hello")).start();
```

2. `run()`

The code executed when the thread runs (don’t call it directly — use `start()`).
```java
class MyThread extends Thread {
  public void run() { System.out.println("Running..."); }
}
```

3. `sleep(ms)`

Pause current thread for given milliseconds.
```java
Thread.sleep(1000); // 1 second pause
```

4. `join()`

Wait for another thread to finish.
```java
t.join(); // main waits until t finishes
```

5. `currentThread()`

Returns the currently executing thread.
```java
System.out.println(Thread.currentThread().getName());
```

6. `getName()` / `setName()`

Get or set thread name.
```java
t.setName("Worker-1");
System.out.println(t.getName());
```

7. `getId()`

Returns unique thread ID.
```java
System.out.println(t.getId());
```

8. `getState()`

Returns the state (NEW, RUNNABLE, BLOCKED, WAITING, etc.).
```java
System.out.println(t.getState());
```

9. `isAlive()`

Checks if thread is still running.
```java
if(t.isAlive()) System.out.println("Still working...");
```

10. `yield()`

Hints scheduler to let other threads run.
```java
Thread.yield();
```

11. `interrupt()`

Sends an interrupt signal to a thread.
```java
t.interrupt();
```

12. `isInterrupted()` / `interrupted()`

Check if a thread was interrupted.
```java
if(Thread.currentThread().isInterrupted()) break;
```

13. `setPriority(int)` / `getPriority()`

Suggest CPU scheduling priority (`1`=MIN, `5`=NORM, `10`=MAX).
```java
t.setPriority(Thread.MAX_PRIORITY);
```

14. `setDaemon(boolean)`

Mark a thread as daemon (ends when all user threads finish).
```java
t.setDaemon(true);
```

15. `activeCount()`

Returns number of active threads in current group.
```java
System.out.println(Thread.activeCount());
```

⚠️ Best practice: use interrupt() + check Thread.interrupted() instead of stop() (unsafe).

---

### Shared Data Problem (Race Conditions)
Threads share memory → risk of corruption if multiple threads write at same time.

Example (bad):
```java
class Counter {
    int count = 0;
    void increment() { count++; }
}

Counter c = new Counter();
Thread t1 = new Thread(() -> { for(int i=0;i<1000;i++) c.increment(); });
Thread t2 = new Thread(() -> { for(int i=0;i<1000;i++) c.increment(); });
t1.start(); t2.start(); t1.join(); t2.join();
System.out.println(c.count); // not always 2000!
```

### Synchronization (Solution)

1. **synchronized** keyword: Only one thread can enter the method at a time.

Example:
```java
class Counter {
    int count = 0;
    synchronized void increment() { count++; }
}
```

2. **Locks**: More flexible than synchronized.

Example:
```java
ReentrantLock lock = new ReentrantLock();
lock.lock();
try { /* critical section */ }
finally { lock.unlock(); }
```

3. **Volatile**: Ensures visibility of variable changes across threads, but doesn’t guarantee atomicity.

Example:
```java
volatile boolean running = true;
```

---

### Communication Between Threads
- wait() / notify()
```java
synchronized(obj) {
    obj.wait();    // wait until notified
    obj.notify();  // wake up a waiting thread
}
```

- BlockingQueue (preferred!)
```java
BlockingQueue<String> q = new LinkedBlockingQueue<>();
new Thread(() -> { try { q.put("data"); } catch(Exception e){} }).start();
System.out.println(q.take());
```

### Executor Framework (Java 5+)
Manages thread pools automatically. Better than creating threads manually.

Example:
```java
ExecutorService pool = Executors.newFixedThreadPool(2);
pool.submit(() -> System.out.println("Task 1"));
pool.submit(() -> System.out.println("Task 2"));
pool.shutdown();
```

### Futures & CompletableFuture
Async programming with callbacks.

Example:
```java
CompletableFuture.supplyAsync(() -> "Hello")
    .thenApply(s -> s + " World")
    .thenAccept(System.out::println);
```

---

### More Modern Java Concurrency

1. Virtual Threads (Java 21+)

Thousands of lightweight threads → ideal for servers.

Example:
```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> System.out.println("Hello from virtual thread"));
}
```

2. Scoped Values (Java 25)

Safer alternative to ThreadLocal.

Example:
```java
ScopedValue<String> USER = ScopedValue.newInstance();
ScopedValue.where(USER, "Rasel").run(() ->
    System.out.println("Running as " + USER.get())
);
```

3. Structured Concurrency (Java 25, preview)

Treat related tasks as one unit, easier cancellation & error handling.

Example:
```java
try (var scope = StructuredTaskScope.open()) {
    var f1 = scope.fork(() -> "Task1");
    var f2 = scope.fork(() -> "Task2");
    scope.join();
    System.out.println(f1.get() + ", " + f2.get());
}
```