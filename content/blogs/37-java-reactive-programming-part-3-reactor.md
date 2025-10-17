---
title: "Reactive Programming in Java - Part 3 (Introduction of Project Reactor and Some Frequently Used Operators)"
description: "Let's learn reactive programming with Java"
date: 2025-10-15
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

---
### Other Parts of This Series:
- **Part 2:** [Reactive Programming in Java - Part 2 (Thinking In Reactive Way and Reative Operator)]({{< ref "blogs/36-java-reactive-programming-part-2-reactive-thinking.md" >}})
- **Part 4:** [Reactive Programming in Java - Part 4 (Other Useful Operators)]({{< ref "blogs/38-java-reactive-programming-part-4-other-operators.md" >}})
---

{{< figure
    src="/img/blogs/35-java-reactive-programming.jpg"
    caption="Reactive Programming (Photo Credit: Reactive Programming Book by Sergi Mansilla)"
    align=center
>}}

In the previous parts we were trying to understand what actually reactive programming is and how its mechanism operates. Also, what does "operator" mean, what are marble diagrams of operators, and how can we start thinking in a reactive way? In this part we will try to explore project **Reactor** and some of its operators and how we can work with them. So, let's start...

---

## Type of Stream/Sequences
Previously we knew reactive programming is all about asynchronous stream processing. And a stream is a sequence of ongoing events ordered in time.

Based on how the reactive stream reacts to subscribers, we can mainly distinguish two broad categories of reactive sequences: **hot** and **cold**.
- A *cold* sequence starts new for each subscriber, including at the source of data. For example, if the source wraps an HTTP call, a new HTTP request is made for each subscription.
- A *hot* sequence does not start from scratch for each subscriber. Rather, late subscribers receive signals emitted after they subscribed. Note, however, that some hot reactive streams can cache or replay the history of emissions totally or partially. From a general perspective, a hot sequence can even emit when no subscriber is listening (an exception to the “nothing happens before you subscribe” rule).

For more information on *hot vs cold* in the context of Reactor, see this [reactor-specific](https://projectreactor.io/docs/core/release/reference/index.html#reactor.hotCold) section.

## Project Reactor, Flux and Mono
**Project Reactor** is the most used library for reactive programming in Java. Spring WebFlux uses this. We will use it as our reactive library for a practical example. **Flux** and **Mono** are two fundamental types to represent sequences of data or events and provide a way to work with asynchronous and non-blocking code.

To use the library project reactor just add the following dependencies in your code:

For Maven:
```xml
<dependency>
    <groupId>io.projectreactor</groupId>
    <artifactId>reactor-core</artifactId>
    <version>{VERSION}</version>
</dependency>
```

For Gradle:
```yml
dependencies {
     implementation 'io.projectreactor:reactor-core' 
}
```

### Flux:
- Flux represents a stream of zero or more items over time. It can emit multiple items.
- It is suitable for scenarios where you expect a sequence of values, such as streaming sensor data, a list of items from a database, or events from multiple sources.
- Flux is analogous to an asynchronous list or iterable.

### Mono:
- Mono represents a stream of exactly zero or one item over time. It can emit a single item or no items (empty).
- It is useful for cases where you expect either a result or an empty response, such as the result of an optional operation, a single value from a database query, or the response to an HTTP request.
- Mono is analogous to a CompletableFuture in Java or a Promise in JavaScript.

## Frequently Used Operators
1. **just & subscribe:**
{{< figure
    src="/img/blogs/37-just-operator.jpeg"
    caption="Marble diagram of just (Photo Credit: Project Reactor)"
    align=center
>}}
The easiest and simplest operator to create an event stream object is just(). It is used to create/convert regular values into objects of Flux or Mono. And remember, reactive programming works in a pub-sub manner, so nothing happens until subscribe().
```java
Mono<String> mono = Mono.just("mono");
mono.subscribe(data -> System.out.println("mono: " + data));

Flux<String> flux = Flux.just("flux-1", "flux-2");
flux.subscribe(data -> System.out.println("flux: " + data));
```

2. **generate:**
{{< figure
    src="/img/blogs/37-generate-operator.png"
    caption="Marble diagram of generate (Photo Credit: Project Reactor)"
    align=center
>}}
generate() is another operator for creating Flux. It takes an exposed API trigger method called sink. And generate() is for synchronous and one-by-one emissions, meaning that the sink is a SynchronousSink and that its next() method can only be called at most once per callback invocation.
```java
Flux<String> flux = Flux.generate(
       () -> 0,
       (state, sink) -> {
          sink.next("3 x " + state + " = " + 3*state);
          if (state == 10) sink.complete();
          return state + 1;
       }, (state) -> System.out.println("state: " + state));
flux.subscribe(data -> System.out.println("data " + data));
```

3. **map:**
{{< figure
    src="/img/blogs/37-map-operator.jpeg"
    caption="Marble diagram of map (Photo Credit: Project Reactor)"
    align=center
>}}
Most of the operator output is the same type of streams that it gets as input. But sometimes we need to return a different type as output. The map() operator does that. It converts all the incoming streams one-by-one by converting them to the desired type as downstream output.
```java
Flux<Integer> flux = Flux.just("1", "2")
       .map(data -> Integer.parseInt(data));
flux.subscribe(data -> System.out.println("data " + data));
```

4. **flatmap:**
{{< figure
    src="/img/blogs/37-flatmap-operator.jpeg"
    caption="Marble diagram of flatmap (Photo Credit: Project Reactor)"
    align=center
>}}
flatmap() is also used to convert an input type into a different type as output. Using the map() method would result in a Mono<Mono<T>>, whereas using flatMap() results in a Mono<T>.
- map is for synchronous, non-blocking, 
- 1-to-1 transformationsflatMap is for asynchronous (non-blocking) 1-to-N transformations.

The difference is visible in the method signature:
- map takes a Function<T, U> and returns a Flux<U>
- flatMap takes a Function<T, Publisher<V>> and returns a Flux<V>.
```java
Flux<Integer> flux = Flux.just("1", "2", "3")
       .flatMap(data -> Mono.just(Integer.parseInt(data)));
flux.subscribe(data -> System.out.println("data " + data));
```

5. **filter:**
{{< figure
    src="/img/blogs/37-filter-operator.png"
    caption="Marble diagram of filter (Photo Credit: Project Reactor)"
    align=center
>}}
Sometimes we need to filter out the streams from our operation based on some condition. filter() does exactly that. It is downstream of the streams if the given condition is true after applying it to the data.
```java
Flux<Integer> flux = Flux.just(1, 2, 3, 4, 5
       .filter(data -> data != 4);
flux.subscribe(data -> System.out.println("data " + data));)
```

6. **doOnNext:**
{{< figure
    src="/img/blogs/37-doOnNext-operator.jpeg"
    caption="Marble diagram of doOnNext (Photo Credit: Project Reactor)"
    align=center
>}}
As its name suggests, doOnNext() executes after Flux emits. It adds behavior (side effect) triggered when the flux emits an item. The consumer is executed first, and then the onNext signal is propagated downstream.
```java
Flux<Integer> flux = Flux.just("1", "2")
       .map(data -> Integer.parseInt(data));
flux.subscribe(data -> System.out.println("data " + data));
```

7. **doOnSuccess:**
{{< figure
    src="/img/blogs/37-doOnSuccess-operator.jpeg"
    caption="Marble diagram of doOnSuccess (Photo Credit: Project Reactor)"
    align=center
>}}
As its name refers, the doOnSuccess() operator is used when we need to perform some task when only the previous step is complete successfully. It adds behavior triggered as soon as the Mono can be considered to have completed successfully.

It takes a consumer as a parameter, and the consumer is executed before propagating either onNext or onComplete downstream. We can use doOnSuccess to attach a listener that will be triggered when the Mono completes successfully.
```java
AtomicInteger a = new AtomicInteger(5);
Mono<Integer> then = Mono.just(10)
		.doOnSuccess(x -> a.addAndGet(x));

then.subscribe(x -> System.out.println(x));
System.out.println(a);
```

8. **switchIfEmpty:**
{{< figure
    src="/img/blogs/37-switchIfEmpty-operator.jpeg"
    caption="Marble diagram of switchIfEmpty (Photo Credit: Project Reactor)"
    align=center
>}}
Sometimes we can get empty or null values from the upstream and need to handle some logic based on emptiness. The switchIfEmpty() operator helps us to do so. It switches to an alternative publisher if this sequence is completed without any data.
```java
Mono<String> defaultMono = Mono.just("defaultString");
Mono<Object> mono = Mono.empty().switchIfEmpty(defaultMono);

mono.subscribe(System.out::println);
```

9. **block:**
{{< figure
    src="/img/blogs/37-block-operator.jpeg"
    caption="Marble diagram of block (Photo Credit: Project Reactor)"
    align=center
>}}
Sometimes we need to male our flow forcefully sync and wait till finish. Subscribe to Mono and block indefinitely until a next signal is received. Returns that value, or null if the Mono completes empty. In case Mono errors, the original exception is thrown (wrapped in a RuntimeException if it was a checked exception). Also note that each block() will trigger a new subscription: in other words, the result might miss signals from hot publishers.
```java
String value = Mono.just("Value")
             .block();
System.out.println(value);
```

10. **handle:**
The handle method is a bit different: it is an instance method, meaning that it is chained on an existing source (as are the common operators). It is close to generate in the sense that it uses a SynchronousSink and only allows one-by-one emissions. However, a handle can be used to generate an arbitrary value out of each source element, possibly skipping some elements. In this way, it can serve as a combination of map and filter.
```java
public static String getAlphabet(int letterNumber) {
    if (letterNumber < 1 || letterNumber > 26) {
       return null;
    }
    int letterIndexAscii = 'A' + letterNumber - 1;
    return "" + (char) letterIndexAscii;
}

public static void operatorTest() {
    Flux<String> alphabets = Flux.just(-1, 30, 13, 9, 20)
          .handle((i, sink) -> {
             String letter = getAlphabet(i);
             if (letter != null)
                sink.next(letter);
          });

    alphabets.subscribe(System.out::println);
}
```

## All Together, Again Thinking in Reactive Way
As we see the above operators and their working mechanisms, they work differently to serve different purposes. We can combine or chain them to fulfill a big purpose. Below we chain up multiple operators all together.
```java
public static String alphabet(int letterNumber) {
    if (letterNumber < 1 || letterNumber > 26) {
       return null;
    }
    int letterIndexAscii = 'A' + letterNumber - 1;
    return "" + (char) letterIndexAscii;
}

public static void operatorTest() {
    Flux<String> alphabet = Flux.just(-1, 30, 13, 9, 20)
          .handle((i, sink) -> {
             String letter = alphabet(i);
             if (letter != null) sink.next(letter);
          })
          .filter(data -> {
             boolean isTrue = !data.equals("M");
             System.out.println(isTrue);
             return isTrue;
          })
          .map(ch -> ch+"-Data")
          .doOnNext(conData -> System.out.println(conData))
          .flatMap(conData -> Mono.just(conData));

    alphabet.subscribe(System.out::println);
}
```
Though we can imagine the outer most operator and subscription, but In Reactor, when we chain operators, we can wrap many Flux and Mono implementations inside one another as we need. Once we subscribe, a chain of Subscriber objects is created, backward (up the chain) to the first publisher. This is effectively hidden from us. All we can see is the outer layer of Flux (or Mono) and Subscription, but these intermediate operator-specific subscribers are where the real work happens.

---

*Insha Allah, in the upcoming part, I will try to explore more operators. Until than, may Allah keep you healthy and happy.*