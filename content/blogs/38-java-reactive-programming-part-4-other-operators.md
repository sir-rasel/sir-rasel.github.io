---
title: "Reactive Programming in Java - Part 4 (Other Useful Operators)"
description: "Let's learn reactive programming with Java"
date: 2025-10-17
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
- **Part 3:** [Reactive Programming in Java - Part 3 (Introduction of Project Reactor and Some Frequently Used Operators)]({{< ref "blogs/37-java-reactive-programming-part-3-reactor.md" >}})
---

{{< figure
    src="/img/blogs/35-java-reactive-programming.jpg"
    caption="Reactive Programming (Photo Credit: Reactive Programming Book by Sergi Mansilla)"
    align=center
>}}

In the previous parts we were trying to understand what actually reactive programming is and how its mechanism operates. Also, we introduced with project Reactor and some of most important operators, what are marble diagrams of operators, and how can we start thinking in a reactive way? In this part we will try to explore other useful operators. So, let's start...

---

## More Useful Operators
1. **defer:**
{{< figure
    src="/img/blogs/38-defer-operator.jpeg"
    caption="Marble diagram of defer (Photo Credit: Project Reactor)"
    align=center
>}}
When we need to capture or create a sequence object lazily, then we should use defer(). It lazily supplies a publisher every time a subscription is made on the resulting Flux/Mono, so the actual source instantiation is deferred until each subscription, and the supplier can create a subscriber-specific instance.
```java
var deferred = Mono.defer(() -> Mono.just(UUID.randomUUID()));

deferred.subscribe(x -> System.out.println(x));
```

2. **blockFirst:**
{{< figure
    src="/img/blogs/38-blockFirst-operator.jpeg"
    caption="Marble diagram of blockFirst (Photo Credit: Project Reactor)"
    align=center
>}}
Subscribe to Flux and block indefinitely until the upstream signals its first value or completes. Returns that value, or null if the Flux completes empty. In case of Flux errors, the original exception is thrown (wrapped in a RuntimeException if it was a checked exception). Note that each blockFirst() will trigger a new subscription: in other words, the result might miss signals from hot publishers.
```java
String first = Flux.just("blue", "green", "red")
       .blockFast();

System.out.println(first);
```

3. **blockLast:**
{{< figure
    src="/img/blogs/38-blockLast-operator.jpeg"
    caption="Marble diagram of blockLast (Photo Credit: Project Reactor)"
    align=center
>}}
Subscribe to Flux and block indefinitely until the upstream signals its last value or completes. Returns that value, or null if the Flux completes empty. In case of Flux errors, the original exception is thrown (wrapped in a RuntimeException if it was a checked exception). Note that each blockLast() will trigger a new subscription: in other words, the result might miss signals from hot publishers.
```java
String last = Flux.just("blue", "green", "red")
       .blockLast();

System.out.println(last);
```

4. **fromCallable:**
{{< figure
    src="/img/blogs/38-fromCallable-operator.jpeg"
    caption="Marble diagram of fromCallable (Photo Credit: Project Reactor)"
    align=center
>}}
It is also used to create sequence objects like Mono lazily. But unlike defer() or just(), fromCallable() creates a Mono producing its value using the provided Callable. If the Callable resolves to null, the resulting Mono completes empty.
```java
var fromCallable = Mono.fromCallable(() -> UUID.randomUUID());
		
fromCallable.subscribe(x -> System.out.println(x));
```

5. **fromSupplier:**
{{< figure
    src="/img/blogs/38-fromSupplier-operator.jpeg"
    caption="Marble diagram of fromSupplier (Photo Credit: Project Reactor)"
    align=center
>}}
It is also similar to defer() and used to create sequence objects like Mono lazily. But a difference is, it can transform the supplied data into Mono automatically. It creates a Mono, producing its value using the provided supplier. If the supplier resolves to null, the resulting Mono completes empty.
```java
var fromSupplier = Mono.fromSupplier(() -> UUID.randomUUID());

fromSupplier.subscribe(x -> System.out.println(x));
```

6. **defaultIfEmpty:**
{{< figure
    src="/img/blogs/38-defaultIfEmpty-operator.jpeg"
    caption="Marble diagram of defaultIfEmpty (Photo Credit: Project Reactor)"
    align=center
>}}
It's closely similar to switchIfEmpty(), but the defaultIfEmpty() indicates the completed sequence. It is used to provide a default unique value if this sequence is completed without any data. Another difference is switchIfEmpty() takes a Flux/Mono stream as input, but defaultIfEmpty() takes a raw value.
```java
Mono<Object> mono = Mono.empty().defaultIfEmpty("defaultValue");

mono.subscribe(System.out::println);
```

7. **distinct:**
{{< figure
    src="/img/blogs/38-distinct-operator.jpeg"
    caption="Marble diagram of distinct (Photo Credit: Project Reactor)"
    align=center
>}}
This operator is also self-describing. The distinct() operator tracks elements for each subscriber and filters out the duplicates. So only the distinct values propagate downstream and remove the duplicate ones.
```java
Flux<String> flux = Flux.just("blue", "blue", "orange", "purple")
       .distinct();

flux.subscribe(System.out::println);
```

8. **fromIterable or fromArray:**
{{< figure
    src="/img/blogs/38-fromIterable-operator.png"
    caption="Marble diagram of fromIterable (Photo Credit: Project Reactor)"
    align=center
>}}
fromIterable() is used for converting an iterable like an array or list to a Flux stream. On the other hand, fromArray() is array-specific, meaning it works with only the array type.
```java
Flux<String> flux = Flux.fromIterable(Arrays.asList("blue", "green", "orange", "purple"));
                    
flux.subscribe(System.out::println);
```

9. **concat and concatMap:**
{{< figure
    src="/img/blogs/38-concat-operator.jpeg"
    caption="Marble diagram of concat (Photo Credit: Project Reactor)"
    align=center
>}}
Concatenate all sources provided in an Iterable, forwarding elements emitted by the sources downstream. Concatenation is achieved by sequentially subscribing to the first source, then waiting for it to complete before subscribing to the next, and so on until the last source completes. Any error interrupts the sequence immediately and is forwarded downstream. It returns a new Flux concatenating all source sequences.

{{< figure
    src="/img/blogs/38-concatMap-operator.jpeg"
    caption="Marble diagram of concatMap (Photo Credit: Project Reactor)"
    align=center
>}}
concatMap() functionality is similar to concat(), which means it concatenates multiple sources and returns a new Flux, but it also maps the items as well. So we can consider it like a combination of the concat() and flatMap() operators.
```java
Flux<Integer> evenNumbers = Flux
			.range(1, 5)
			.filter(x -> x % 2 == 0);

Flux<Integer> oddNumbers = Flux
			.range(1, 5)
			.filter(x -> x % 2 > 0);

Flux<Integer> fluxOfIntegers = Flux.concat(evenNumbers, oddNumbers);
fluxOfIntegers.subscribe(x -> System.out.println(x));

Flux<String> mergedFlux = Flux.just(1, 2, 3)
	.concatMap(it -> Mono.just(it.toString().concat(": n")));
mergedFlux.subscribe(x -> System.out.println(x));
```

10. **zip and zipWith:**
{{< figure
    src="/img/blogs/38-zip-operator.jpeg"
    caption="Marble diagram of zip (Photo Credit: Project Reactor)"
    align=center
>}}
Like its name says, the zip() operator combines or zips multiple sources together; that is to say, it waits for all the sources to emit one element and combines these elements once into an output value (constructed by the provided combinator). The operator will continue doing so until any of the sources are completed. Errors will immediately be forwarded. This "Step-Merge" processing is especially useful in Scatter-Gather scenarios.

{{< figure
    src="/img/blogs/38-zipWith-operator.jpeg"
    caption="Marble diagram of zipWith (Photo Credit: Project Reactor)"
    align=center
>}}
Zip this Flux with another publisher source; that is to say, wait for both to emit one element and combine these elements once into a Tuple2. The operator will continue doing so until any of the sources are completed. Errors will immediately be forwarded. This "Step-Merge" processing is especially useful in Scatter-Gather scenarios.
```java
Flux<Integer> evenNumbers = Flux
			.range(1, 5)
			.filter(x -> x % 2 == 0);

Flux<Integer> oddNumbers = Flux
			.range(1, 5)
			.filter(x -> x % 2 > 0);

Flux<Tuple2<Integer, Integer>> fluxOfIntegers = Flux.zip(evenNumbers, oddNumbers);
fluxOfIntegers.subscribe(x -> System.out.println(x));

Flux<Tuple2<Integer, Integer>> flux = evenNumbers.zipWith(oddNumbers);
flux.subscribe(x -> System.out.println(x));
```

11. **then and thenEmpty:**
{{< figure
    src="/img/blogs/38-then-operator.jpeg"
    caption="Marble diagram of then (Photo Credit: Project Reactor)"
    align=center
>}}
then() is used when you don't care about what elements a publisher has output; you only care about when it finishes. So it takes an existing publisher, throws all of its elements away, and then propagates the completion signal or error signals. If we pass any Mono as a parameter of then(), it will propagate the parameter Mono as output.

{{< figure
    src="/img/blogs/38-thenEmpty-operator.jpeg"
    caption="Marble diagram of thenEmpty (Photo Credit: Project Reactor)"
    align=center
>}}
It is also like then(), but the difference is that thenEmpty() not only returns a Mono<Void>, but it also takes a Mono<Void> as a parameter. It represents a concatenation of the source completion signal and then the second, empty Mono completion signal. In other words, it completes when A and then B have both completed sequentially and doesn't emit data.
```java
Mono<Void> then = Flux.just("blue", "green", "red")
		  .then(Mono.just("Orange"))
		  .thenEmpty(Mono.empty());
then.subscribe();
```

12. **merge:**
{{< figure
    src="/img/blogs/38-merge-operator.png"
    caption="Marble diagram of merge (Photo Credit: Project Reactor)"
    align=center
>}}
merge() is a similar operator to concat() or zip(), which is used to combine the results or sequences. But there is a difference: merge() can combine different data-type sequences into a single sequence. It merges data from publisher sequences contained in an iterable into an interleaved merged sequence. Unlike concat, inner sources are subscribed to eagerly. A new iterator will be created for each subscriber.
```java
Flux<Integer> evenNumbers = Flux
			.range(1, 5)
			.filter(x -> x % 2 == 0);

Flux<String> oddNumbers = Flux
			.range(1, 5)
			.filter(x -> x % 2 > 0)
			.map(x -> x.toString().concat(": n"));

var flux1 = Flux.merge(evenNumbers, oddNumbers);
flux1.subscribe(x -> System.out.println(x));
```

---

*Insha Allah, in the upcoming part and last part of this series, I will try to explore error handling operators. Until than, may Allah keep you healthy and happy.*