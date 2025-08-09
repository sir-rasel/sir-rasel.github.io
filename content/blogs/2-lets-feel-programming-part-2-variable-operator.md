---
title: "Let's Feel Programming Fundamentals - Part 2 (Variable, Operator)"
description: "You will be a superstar once you begin to feel programming"
date: 2025-08-08
tags: ["programming", "programming-basic", "programming-fundamentals", "data-type", "variable", "constant", "opeartor"]
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
    image: "img/blogs/2-datatypes-cpp.jpg"
    caption: "programming"
    alt: "programming"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
**Part 1:** [Let's Feel Programming Fundamentals - Part 1]({{< ref "blogs/1-lets-feel-programming-part-1.md" >}})

---

# Data Type, Variable & Constant
{{< figure
    src="/img/blogs/2-datatypes-cpp.jpg"
    caption="C++ Data Types (Photo Credit: Sitesbay)"
    align=center
>}}

## Story
Once upon a time, Alice and Bob was 2 friends. Their friendship was so famous in that time. One day, they were deciding to go for a trip in the Space. Now they need to carry some necessary things for their trip (like: food, water etc.). So they started keeping the things as follows:

- Point 1: They carried oxygen in a cylinder.
- Point 2: They carried water in bottle, those were in different size.
- Point 3: They carried dry food in a bag, those were in different size.
- Point 4: They carried some materials those only could be used but not change its quantity.
- Point 5: For safety reason they carried a special plastic bag that can hold water, oxygen, dry food or any type of materials. 

## Data Type
It is nothing but the oxygen, water, dry food in the above mentioned point 1, 2 and 3. Means data type defines the ***type of a data***. It describes the *data shape* means is it a real number or decimal? Is it a string or single characters? Or is it like void means nothing? Suppose we can say oxygen as void, water as string and dry food as number etc. And same type data can be vary as its size, like we can see at point 2 and 3. Then we need bigger size bottle or bag to carry those. **Int, Double, String, Long, Void, Bool** are some well known primitive data type exist in different programming language.

## Variable
It can be consider as a ***container*** that can hold the different data of different types. Different container is being used for different types of data. In the above story cylinder, bottle, bag can be said as variable in point 1, 2 and 3. We can not carry out oxygen in bag and dry food in cylinder. So variable is the container that can holds data of different type and its amount of data can vary over time. It means after eating some food or drinking some water the amount is being vary. Some programming language supports a dynamic type variable declaration that can hold any type of data like point 5.

## Constant
In point 4, we see some materials that can be used but can not changed its quantity. Means, like water or food we can not eat or drink them and reduced in quantity. But if we consider hammer as such materials here, it can be used for different purpose but its quantity is not vary. So **constant** in programming is something that is not vary or changed. Means after the first declare and initialization its value is never being changed. Generally we define a constant variable by ***"const"*** keyword.

---

# Operator
{{< figure
    src="/img/blogs/2-operators-cpp.png"
    caption="C++ Operators (Photo Credit: Dot Net Tutorials)"
    align=center
>}}

## Story
Rahim, Karim and Babul are working in a factory called kopaSamsu. Here they work as a machine operator and their primary duty is operating their respective machines. Now consider the followings:

- Point 1: Rahim is operating those type of machine whom are pairwise. That is machinery that works together to perform a task. They called them by different names like: logical machine, relational machine and arithmetic machine. And Rahim known as binary operator.
- Point 2: Karim is operating a single machine and unlike Rahim and Babul his machine can work individually. They called them increment/decrement machines. And Karim is known as a unary operator.
- Point 3: Babul is operating a machine that has 3 machines combined together. Babul is known as ternary operator.

## Operators
Operator in programming is nothing but a *special one that operates on something called operand*. After operations they produce something based on operands. In the above story Rahim, Karim and Babul are operators and machines are operands. And our operator's friend produces results based on their machines. 

According to the tutorials point website ***"An operator in a programming language is a symbol that tells the compiler or interpreter to perform specific mathematical, relational or logical operation and produce final result"***.

Based on the number of operands, operators in programming operators can be 3 types. Like:

1. **Binary operator**: as name refers, it working with 2 operands. Then the expression looks like (**operand1 operator operand2**). In point 1, is an example of binary operator operation. Some binary operators are logical operator (&&, || ), relational operator (<, >, ==), arithmetic operator (+, -, *, /).
2. **Unary operator**: as name refers, it working with only one operator. Then the expression looks like (**operandOperator or operatorOperand**). In point 2, is an example of unary operator operation. Some unary operators are logical operator (!), increment operator (++), decrement operator (--).
3. **Ternary operator**: as name refers, it working with three operator. Then the expression looks like (**operand1 ? operand2 : operand3**). in point 3, is an example of ternary operator operation. Ternary operator is conditional operator (? : ).
---
## Code Example (C++)
```c++
#include <iostream>
using namespace std;

int main() {
    // === Data Types & Variables ===
    int age = 25;               // Integer type
    float height = 5.9;         // Floating point type
    char grade = 'A';           // Character type
    bool isPassed = true;       // Boolean type
    double pi = 3.1415926535;   // Double precision floating point

    // === Constant ===
    const int MAX_SCORE = 100;  // Constant value (cannot be changed)

    // === Operators ===

    // Arithmetic operators
    int a = 10, b = 3;
    int sum = a + b;            // Addition
    int diff = a - b;           // Subtraction
    int product = a * b;        // Multiplication
    int quotient = a / b;       // Division
    int remainder = a % b;      // Modulo

    // Relational operators
    bool isEqual = (a == b);
    bool isGreater = (a > b);

    // Logical operators
    bool result = (isPassed && (age < 30));

    // Output results
    cout << "Age: " << age << endl;
    cout << "Height: " << height << endl;
    cout << "Grade: " << grade << endl;
    cout << "Passed: " << isPassed << endl;
    cout << "Pi: " << pi << endl;
    cout << "Max Score: " << MAX_SCORE << endl;

    cout << "\nArithmetic Operations:\n";
    cout << "Sum: " << sum << endl;
    cout << "Difference: " << diff << endl;
    cout << "Product: " << product << endl;
    cout << "Quotient: " << quotient << endl;
    cout << "Remainder: " << remainder << endl;

    cout << "\nRelational & Logical Operations:\n";
    cout << "Is Equal: " << isEqual << endl;
    cout << "Is Greater: " << isGreater << endl;
    cout << "Result (isPassed && age < 30): " << result << endl;

    return 0;
}
```

---

*Insha Allah, in the upcoming blogs we will deep dive other fundamental concepts. Until than, may Allah keep you healthy and happy.*