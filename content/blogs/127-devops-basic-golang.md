---
title: "DevOps - Step By Step Learning : Part 4 (Basic Programming Using Golang)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-16T00:00:00Z"
tags: ["devops" , "golang", "GO"]
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
    image: "img/blogs/127-devops-basic-golang.jfif"
    caption: "DevOps Basic Golang Programming"
    alt: "DevOps Basic Golang Programming"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 3:** [DevOps - Step By Step Learning : Part 3 (A Simplified Roadmap to Start)]({{< ref "blogs/126-devops-roadmap.md" >}})
---

{{< figure
    src="/img/blogs/127-devops-basic-golang.jfif"
    caption="DevOps Basic Golang Programming (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

The roadmap defined was done, and it's time to start learning accordingly. The first step was learning a programming language. Though Rasel was working on C# (.NET), he decided to learn a new lightweight and faster language and picked **Golang**. Because Golang is lightweight, faster, and cloud-native. Many DevOps tools, like Docker and Kubernetes, are built using Golang.

As Rasel knows the programming fundamentals, it was easy to cross-check and learn it in the earliest time.

* * *

## Programming Fundamentals:

In every programming language, basically the following **fundamental things** are the backbone:

- **Part 1:** [Let's Feel Programming Fundamentals - Part 1]({{< ref "blogs/1-lets-feel-programming-part-1.md" >}})
- **Part 2:** [Let's Feel Programming Fundamentals - Part 2 (Variable, Operator)]({{< ref "blogs/2-lets-feel-programming-part-2-variable-operator.md" >}})
- **Part 3:** [Let's Feel Programming Fundamentals - Part 3 (Condition, Loop)]({{< ref "blogs/3-lets-feel-programming-part-3-condition-loop.md" >}})
- **Part 4:** [Let's Feel Programming Fundamentals - Part 4 (Function, Pointer, Scope)]({{< ref "blogs/4-lets-feel-programming-part-4-function-pointer.md" >}})
- **Part 5:** [Let's Feel Programming Fundamentals - Part 5 (Procedural, Functional, OOP Style)]({{< ref "blogs/5-lets-feel-programming-part-5-programming-style.md" >}})
- **Part 6:** [Let's Feel Programming Fundamentals - Part 6 (Data Structure)]({{< ref "blogs/6-lets-feel-programming-part-6-data-structure.md" >}})
- **Part 7:** [Let's Feel Programming Fundamentals - Part 7 (Algorithm)]({{< ref "blogs/7-lets-feel-programming-part-7-algorithm.md" >}})
- **Part 8:** [Let's Feel Programming Fundamentals - Part 8 (Threads, Async-await, Concurrency, Parallel)]({{< ref "blogs/8-lets-feel-programming-part-8-concurrency-parallel.md" >}})

## How to these Concepts Works in Golang:

***Data Types, Variables, and Constants***

*   Data Types: Go has basic types like int, string, bool, and float64.
*   Variables: Declared using var or := (short-hand declaration).
*   Constants: Declared using const, and their values cannot change.

```go
package main
import "fmt"

func main() {
    var age int = 25       // Integer variable
    name := "John"         // String variable (short-hand)
    const pi float64 = 3.14 // Constant value

    fmt.Println("Age:", age)
    fmt.Println("Name:", name)
    fmt.Println("Pi:", pi)
}        
```

***Operators***

*   Arithmetic Operators: +, -, \*, /, %
*   Relational Operators: ==, !=, <, >, <=, >=
*   Logical Operators: &&, ||, !
*   Assignment Operators: =, +=, -=, \*=, /=

```go
package main
import "fmt"

func main() {
    a, b := 10, 5
    fmt.Println("Addition:", a+b)  // Arithmetic
    fmt.Println("Greater than:", a > b)  // Relational
    fmt.Println("Logical AND:", (a > 5) && (b < 10))  // Logical
}        
```

***Condition (if-else & switch)***

*   Used for decision-making.

```go
package main
import "fmt"

func main() {
    num := 10

    if num > 0 {
        fmt.Println("Positive number")
    } else if num < 0 {
        fmt.Println("Negative number")
    } else {
        fmt.Println("Zero")
    }

    // Switch case
    day := 3
    switch day {
    case 1:
        fmt.Println("Monday")
    case 2:
        fmt.Println("Tuesday")
    default:
        fmt.Println("Other day")
    }
}        
```

***Loop (for loop)***

*   Go only has for loops (it replaces while and do-while).

```go
package main
import "fmt"

func main() {
    // Standard for loop
    for i := 1; i <= 5; i++ {
        fmt.Println("Iteration:", i)
    }

    // Loop through an array
    numbers := []int{10, 20, 30}
    for index, value := range numbers {
        fmt.Println("Index:", index, "Value:", value)
    }
}        
```

***Function***

*   Functions help organize reusable code.

```go
package main
import "fmt"

// Function with parameters and return value
func add(a int, b int) int {
    return a + b
}

func main() {
    sum := add(10, 5)
    fmt.Println("Sum:", sum)
}        
```

***Memory Allocation and Pointers***

*   Pointers store memory addresses.
*   new() allocates memory dynamically.

```go
package main
import "fmt"

func main() {
    x := 10
    p := &x  // Pointer to x

    fmt.Println("Value of x:", x)
    fmt.Println("Memory address of x:", p)
    fmt.Println("Value via pointer:", *p)  // Dereferencing
}        
```

***Variable Lifetime and Scope***

*   Global variables exist throughout the program.
*   Local variables exist only inside functions.

```go
package main
import "fmt"

// Global variable
var globalVar = "I am global"

func main() {
    localVar := "I am local" // Local variable
    fmt.Println(globalVar)
    fmt.Println(localVar)
}        
```

***Object-Oriented Concepts (Structs & Methods)***

*   Structs are like objects in Go.
*   interfaces are the declarations of function prototypes that can implemented.
*   Methods are functions attached to structs.

```go
package main
import "fmt"

// Struct definition
type Car struct {
    brand string
    year  int
}

// Interface definition
type Speaker interface {
  Speak() string
}

// Method associated with Car struct
func (c Car) display() {
    fmt.Println("Brand:", c.brand, "Year:", c.year)
}

func main() {
    myCar := Car{"Toyota", 2022}
    myCar.display()  // Calling method
}        
```

***Data Structures***

*   Array: Fixed size
*   Slice: Dynamic array
*   Map: Key-value pairs

```go
package main
import "fmt"

func main() {
    // Array
    var arr = [3]int{1, 2, 3}
    fmt.Println("Array:", arr)

    // Slice
    slice := []int{10, 20, 30}
    slice = append(slice, 40)  // Append new element
    fmt.Println("Slice:", slice)

    // Map (key-value pairs)
    person := map[string]int{"Alice": 25, "Bob": 30}
    fmt.Println("Bob's age:", person["Bob"])
}        
```

***Algorithm (Sorting Example)***

*   Implementing Bubble Sort algorithm.

```go
package main
import "fmt"

func bubbleSort(arr []int) {
    n := len(arr)
    for i := 0; i < n-1; i++ {
        for j := 0; j < n-i-1; j++ {
            if arr[j] > arr[j+1] {
                arr[j], arr[j+1] = arr[j+1], arr[j]
            }
        }
    }
}

func main() {
    numbers := []int{64, 25, 12, 22, 11}
    bubbleSort(numbers)
    fmt.Println("Sorted array:", numbers)
}        
```

***Concurrency (Goroutines & Channels)***

*   Goroutines allow parallel execution.
*   Channels enable safe communication.

```go
package main
import (
    "fmt"
    "time"
)

// Goroutine function
func sayHello() {
    time.Sleep(2 * time.Second)
    fmt.Println("Hello from Goroutine!")
}

func main() {
    go sayHello()  // Runs concurrently
    fmt.Println("Main function execution")
    time.Sleep(3 * time.Second) // Wait to see goroutine output

   ch := make(chan int) // channel
   go func() {
      ch <- 42
   }()
   fmt.Println(<-ch) // receive from channel
}        
```

Besides all of this, *error handling, testing, generics* are also advanced topics should be learned.

* * *

## Summary:

Go (Golang) is a simple and efficient programming language with strong support for concurrency and performance. It has basic data types like int, string, bool, and float64, and allows you to store values in variables or constants (which don’t change). You can perform calculations and comparisons using operators such as +, -, ==, and &&. To make decisions, Go provides conditional statements like if, else, and switch, while repetitive tasks can be handled using loops, mainly the for loop.

Functions help break code into reusable blocks, and Go uses structs, methods and interfaces instead of traditional classes for object-oriented programming. Go also provides pointers to store memory addresses, and variables have lifetime and scope, meaning they exist for a certain time and in a certain part of the program. Data in Go can be organized using data structures like arrays, slices, maps, and structs, while algorithms define step-by-step solutions to problems.

A standout feature of Go is concurrency, allowing multiple tasks to run at the same time using goroutines and channels. This makes Go ideal for building fast, scalable applications. Overall, Go is designed to be simple, fast, and highly efficient, making it great for web development, cloud computing, and system programming.

### Further readings:
- https://go.dev/doc/
- https://go.dev/doc/tutorial/getting-started
- https://gobyexample.com