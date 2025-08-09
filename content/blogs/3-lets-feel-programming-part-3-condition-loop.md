---
title: "Let's Feel Programming Fundamentals - Part 3 (Condition, Loop)"
description: "You will be a superstar once you begin to feel programming"
date: 2025-08-09
tags: ["programming", "programming-basic", "programming-fundamentals", "condition", "loop"]
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
    image: "img/blogs/3-condition-loop.jpeg"
    caption: "programming"
    alt: "programming"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Let's Feel Programming Fundamentals - Part 2 (Variable, Operator)]({{< ref "blogs/2-lets-feel-programming-part-2-variable-operator.md" >}})
- **Part 4:** [Let's Feel Programming Fundamentals - Part 4 (Function, Pointer, Scope)]({{< ref "blogs/4-lets-feel-programming-part-4-function-pointer.md" >}})
---

# Condition & Loop
{{< figure
    src="/img/blogs/3-condition-loop.jpg"
    caption="C++ Condition & Loop (Photo Credit: Medium)"
    align=center
>}}

Conditions and Loops that help in decision-making and doing some work again and again, respectively. Without these 2, programming is nothing. Let's explore them in detail.

# Condition
{{< figure
    src="/img/blogs/3-condition.png"
    caption="C++ Condition (Photo Credit: BBC)"
    align=center
>}}

## Story
One day Alice and Bob go to a super shop to buy chocolate. Alice takes $10 and Bob takes $15 for buying chocolate. They come near to the chocolate shelf and start choosing chocolate to buy. Different sizes of chocolate are labeled with their price, like the big one is $20, the medium one is $15, and the small one is $10. Now Alice starts choosing chocolate based on his capability. 

- Point 1: If the big one is $5-10, then he buys the big chocolate.
- Point 2: Else if the medium one is $10-12, then he buys the medium chocolate.
- Point 3: Otherwise, he buys the small one.

Now Bob starts choosing chocolate based on his capability and style.

- Point 4: He picks a big one and matches the price with his capability; if they match, then he buys it. Otherwise, pick the medium one and match the price. If they match, then buy the medium one. If it does not match with the medium one, then pick the small one that matches and buy the small one with a similar procedure.


## Conditions
In programming, a condition is simply the selection of one or more items from a set, depending on some criterion. It is used for making decisions based on various options. 

According to Wikipedia, ***In computer science, conditions (that is, conditional statements, conditional expressions, and conditional constructs) are programming language commands for handling decisions. Specifically, conditionals perform different computations or actions depending on whether a programmer-defined boolean condition evaluates to true or false.*** 

In programming, we handle conditions in two ways.  One approach is to use if...else-if...else. Another option is to switch the case style.  Points 1, 2, and 3 in the preceding example demonstrate the if...else approach.  Point 4 refers to the switch-case style.  The sole difference between these two types is that switch cases only match values that are equal, but if-else can handle any type of conditional logic.

---

# Loop
{{< figure
    src="/img/blogs/3-loop.png"
    caption="C++ Loop (Photo Credit: BBC)"
    align=center
>}}

## Story
Josh and Jack are two close friends. They both have girlfriends called Alica and Jasmine, respectively. They are also friends of each other. Now one day both of the couple plan for a date and fix an ideal date and time. But as Josh and Jack are both very lazy, they become late on that day for dating.

Then as a punishment their girlfriends decide as follows:
- Point 1: Alica tells Josh to buy a rose and say I love you, and do the things 10 times.
- Point 2: Jasmine tells Jack to buy a rose and say "I love you," while Jasmine's ego is not satisfied.
- Point 3: Additionally, both Alica and Jasmine asked to kiss them at least once, and they said not to stop.

## Loops
In simple words, "loop" means "again and again". When similar things happen again and again, then we can call this a loop. In programming, a loop is something that is being used to execute a similar code or functionality again and again. 

According to Wikipedia, ***In computer science, a loop is a control flow statement for specifying, which allows code to be executed repeatedly.*** 

In the above story, points 1, 2, and 3 are the examples of loops. Generally, there are 3 types of loops that exist in any programming language.

- **For loop:** Ideally in a for loop we do a job for a fixed number of times. Point 1 is an example of a for loop.
- **While loop:** Ideally in while loop we do a job until a certain condition is fulfilled. Point 2 is an example of a while loop.
- **Do...While loop:** When we need a job done until a certain condition is fulfilled, but we want the job done at least once, then we use the do…while loop. Point 3 is an example of a do…while loop.

---
## Code Example (C++)
```c++
#include <iostream>
using namespace std;

int main() {
    int secretNumber = 7;
    int guess;

    cout << "Guess the secret number between 1 and 10:\n";

    // Loop: Keep running until the user guesses correctly
    while (true) {
        cout << "Enter your guess: ";
        cin >> guess;

        // Condition: Check if the guess is correct
        if (guess == secretNumber) {
            cout << "Congratulations! You guessed the correct number.\n";
            break;  // Exit the loop
        } else {
            cout << "Wrong guess. Try again.\n";
        }
    }

    return 0;
}
```

---

*Insha Allah, in the upcoming blogs we will deep dive other fundamental concepts. Until than, may Allah keep you healthy and happy.*