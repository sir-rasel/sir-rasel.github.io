---
title: "Reactive Programming in Java - Part 5 (Error Handling in Reactor and Conclusion)"
description: "Let's learn reactive programming with Java"
date: 2025-10-18
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
- **Part 4:** [Reactive Programming in Java - Part 4 (Other Useful Operators)]({{< ref "blogs/38-java-reactive-programming-part-4-other-operators.md" >}})
---

{{< figure
    src="/img/blogs/36-reactive-programming.jpeg"
    caption="Reactive Programming (Photo Credit: zibtek.com)"
    align=center
>}}

In the previous parts we were trying to learn everything need to start the reactive programming. In this part we will try to explore how to handle error in Reactor. So, let's start...

---

## Error Handling Operators
1. **onError Callback:**

Suppose we need to do something when an error occurs by catching it from the try...catch block. The ideal case in regular programming is something that looks like the example below:
```java
try {
  System.out.println("Success");
} catch (Throwable t) {
    System.err.println("Failed"); 
}
```

So how can we do something similar in reactive programming? There are many ways to do so. One of them is the onError callback of the subscribe() operator. The subscribe() operator takes an error callback as its 2nd parameter, like below:
```java
Flux<String> s = Flux.range(1, 10)
    .map(v -> doSomethingDangerous(v)) 
    .map(v -> doSecondTransform(v)); 
s.subscribe(value -> System.out.println("Success"), 
            error -> System.err.println("Failed") 
);
```

2. **doOnError:**
{{< figure
    src="/img/blogs/39-doOnError-operator.jpeg"
    caption="Marble diagram of doOnError (Photo Credit: Project Reactor)"
    align=center
>}}
It is more like the onError callback that we discussed earlier. But in a more convenient way. For example, we have a scenario like the one below:
```java
try {
  return callExternalService(k);
}
catch (RuntimeException error) {
  //make a record of the error
  log("uh oh, falling back, service failed for key " + k);
  throw error;
}
```

We can do the similar thing using doOnError() operator. For example:
```java
LongAdder failureStat = new LongAdder();
Flux<String> flux =
Flux.just("unknown")
    .flatMap(k -> callExternalService(k) 
        .doOnError(e -> {
            failureStat.increment();
            log("uh oh, falling back, service failed for key " + k); 
        })
        
    );
```

3. **onErrorReturn:**
{{< figure
    src="/img/blogs/39-onErrorReturn-operator.jpeg"
    caption="Marble diagram of onErrorReturn (Photo Credit: Project Reactor)"
    align=center
>}}
Sometimes we need to return something by catching the error. For example,
```java
try {
  return doSomethingDangerous(10);
}
catch (Throwable error) {
  return "RECOVERED";
}
```

We can do so using the onErrorReturn() operator in the below way:
```java
Flux.just(10)
    .map(this::doSomethingDangerous)
    .onErrorReturn("RECOVERED");
```

4. **onErrorComplete:**
{{< figure
    src="/img/blogs/39-onErrorComplete-operator.png"
    caption="Marble diagram of onErrorComplete (Photo Credit: Project Reactor)"
    align=center
>}}
There can occur a situation when we are just concerned about the success and ignore the exception. And just want to complete the task, whatever success or error happens. Like:
```java
try {
  return doSomethingDangerous(30);
}
catch (Throwable error) {
}
```

We can achieve the above condition by using the onErrorComplete() operator. For example:
```java
Flux.just(10,20,30)
    .map(this::doSomethingDangerousOn30)
    .onErrorComplete(); 
```

5. **onErrorMap:**
{{< figure
    src="/img/blogs/39-onErrorMap-operator.jpeg"
    caption="Marble diagram of onErrorMap (Photo Credit: Project Reactor)"
    align=center
>}}
Sometimes we want to throw or map the current exception into another type of exception and rethrow it. For example:
```java
try {
  return callExternalService(k);
}
catch (Throwable error) {
  throw new BusinessException("oops, SLA exceeded", error);
}
```

Reactor gives us a way to do so by the onErrorMap() operator. Like:
```java
Flux.just("timeout1")
    .flatMap(k -> callExternalService(k))
    .onErrorMap(original -> new BusinessException("oops, SLA exceeded", original));
```

6. **onErrorResume:**
{{< figure
    src="/img/blogs/39-onErrorResume-operator.jpeg"
    caption="Marble diagram of onErrorResume (Photo Credit: Project Reactor)"
    align=center
>}}
If you want more than a single default value and you have an alternative (safer) way of processing your data, you can use onErrorResume(). This would be the equivalent of “Catch and execute an alternative path with a fallback method.” For example, if your nominal process is fetching data from an external and unreliable service but you also keep a local cache of the same data that can be a bit more out of date but is more reliable, you could do the following:
```java
String v1;
try {
  v1 = callExternalService("key1");
}
catch (Throwable error) {
  v1 = getFromCache("key1");
}

String v2;
try {
  v2 = callExternalService("key2");
}
catch (Throwable error) {
  v2 = getFromCache("key2");
}
```

The following example shows the Reactor equivalent:
```java
Flux.just("key1", "key2")
    .flatMap(k -> callExternalService(k) 
        .onErrorResume(e -> getFromCache(k)) 
    );
```

7. **doFinally:**
{{< figure
    src="/img/blogs/39-doFinally-operator.jpeg"
    caption="Marble diagram of doFinally (Photo Credit: Project Reactor)"
    align=center
>}}
There always occurs a situation when we need to do something after a successful or error-handling operation. Traditionally we do so using the finally operator. For example:
```java
Stats stats = new Stats();
stats.startTimer();
try {
  doSomethingDangerous();
}
finally {
  stats.stopTimerAndRecordTiming();
}
```

In Reactor, we have an operator called doFinally() that gives us the same opportunity. Like:
```java
Stats stats = new Stats();
LongAdder statsCancel = new LongAdder();

Flux<String> flux =
Flux.just("foo", "bar")
    .doOnSubscribe(s -> stats.startTimer())
    .doFinally(type -> { 
        stats.stopTimerAndRecordTiming();
        if (type == SignalType.CANCEL) 
          statsCancel.increment();
    });
```

---

### Conclusion
As we saw, reactive programming is a very good programming paradigm that has a clean functional programming style called "operators" and gives a non-blocking, backpressure, and efficient way of programming. This is a very good choice for large-scale, high-traffic, and large-data applications. To work with reactive programming, we need to grow reactive thinking and a mindset. And we can achieve this thinking capability by deep diving into the details of reactive programming and gathering knowledge.

### Further Resources:
- [Project Reactor docs](https://projectreactor.io/docs/core/release/reference/gettingStarted.html)
- [How to read marble diagram](https://projectreactor.io/docs/core/release/reference/apdx-howtoReadMarbles.html#page-title)
- [Which operator do I need](https://projectreactor.io/docs/core/release/reference/apdx-operatorChoice.html#page-title)
- [Flux](https://projectreactor.io/docs/core/release/api/reactor/core/publisher/Flux.html)
- [Mono](https://projectreactor.io/docs/core/release/api/reactor/core/publisher/Mono.html)
- [Mastering Java Reactive Programming Course](https://www.udemy.com/course/complete-java-reactive-programming/)

Hope you enjoy the series and best of luck for your reactive programming journey.