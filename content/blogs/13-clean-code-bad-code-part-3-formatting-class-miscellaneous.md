---
title: "Writing Clean Code - Part 3 (Formatting, Class & Object, Miscellaneous)"
description: "Let's learn how can we write good class, object, and format code"
<<<<<<< HEAD
date: 2025-08-20
=======
date: 2025-08-19
>>>>>>> 5caba29 (Add 13th post)
tags: ["programming", "programming-basic", "clean-code", "code-smell", "bad-smell", "formatting", "class-object"]
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
    image: "img/blogs/13-clean-code-formatting.png"
    caption: "clean code"
    alt: "clean code"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Writing Clean Code - Part 2 (Name, Function, Comment)]({{< ref "blogs/12-clean-code-bad-code-part-2-name-function-comment.md" >}})
---

{{< figure
    src="/img/blogs/13-clean-code-formatting.png"
    caption="Clean Code - Formatting, Class & Object, Miscellaneous (Photo Credit: Sotatek)"
    align=center
>}}

Remember 2 things:
1. The only measurement of your code is WTFs / Minute. That is what the readers feel when reviewing code.
2. Linux Torvalds, the creator of the Linux operating system, says, ***“Talk is cheap; show me the code.”***

So if we connect the above 2 points, then we can easily understand that our code should be talkable and self-describing because when anyone reviews/reads our code, they should feel well and comfortable enough. 

In this section we are talking about the ways we can write clean code and avoid the badness/WTFs of our code.

## Formatting
As the main purpose of clean code is increasing readability and maintainability, formatting our code is quite helpful to do so. Formatting our code in the right way makes our code more readable and makes our life easy. 

Below are some tips for writing clean formatting:

1. How big should a source file be? The answer is it should be as small as possible. Ideally 40-400 lines. But it can be any number of lines while maintaining the single responsibility principle.
2. The content of a file should maintain the important things first in a top-down approach; that means vertically sorted in terms of use and importance of the content.
3. Separate the concern with a blank line. It means grouping the related lines together and separating the groups by a blank line.
4. Lines of code that are tightly related should appear close enough and dense.
5. Variables should be declared as close to their uses as possible.
6. Instance variables of a class should be declared at the beginning of the class.
7. Class methods should come after all the instance variables.
8. Public property can be instance variables or methods and should come before the private ones.
9. Functions that are dependent on each other should come as closeas possible. And ideally in a top-to-bottom manner.
10. How wide should a line be? The answer is again as small as possible. It should fit in one window of the editor without scrolling to the right side.
11. Separate the closely related contents with commas and spaces.
12. Our code should be properly aligned and indented for all levels. Indentation is the key to formatting code.
13. All blocks should maintain the open and close braces even for dummy use without a block body.
14. And after all, maintain all the formatting rules defined by the team you work with.

### Final Word (formatting):
Code formatting is important. It is too important to ignore, and it is too important to treat religiously. Code formatting is about communication, and communication is the professional developer’s first order of business. So maintaining code formatting leads you to the clean and professional coder.

## Class and Object
As we already know, a class is a blueprint or type declaration of an object, and an object is a variable of class type. We all use them regularly and frequently in our code. 

Below are some tips for writing clean classes and objects:

1. First of all, a class should be as small as possible. Its length should be between readable and scrollable states.
2. Use more and more abstraction and encapsulation whenever possible.
3. A class always should be maintained. SRP means single responsibility principle. One and only one responsibility per class.
4. We need to maintain high cohesion and less coupling as much as possible.
5. A class should have its private properties declared first and then its public ones.
6. A class should be extensible and closed for modification.
7. An object should be created only when it is needed.
8. An object exposes behaviors and hides data.
9. Maintain the law of Demeter.

### Final Word (class & object)
In a real-world software program, all things are the combination of class and objects. So writing a good, clean, and well-designed class and its objects is a milestone for one software engineer. Mastering it makes you a superior programmer.

## Miscellaneous
1. Consider exception handling as a separate concern; for handling errors, use exceptions, meaning try-catch-finally blocks, instead of just returning codes or messages.
2. Handle catching specific errors as much as possible, and always keep a last wildcard check, which means a generic catch block at last, so that it can handle the error at last if all of the specified catch blocks failed to catch the error.
3. Provide enough context and a proper message when you throw an exception.
4. Always avoid returning NULL as much as possible. Because the majority of our software program errors have occurred due to the null reference exception. So try to avoid returning NULL if our code does not demand it.
5. Clean up the code that is not in use and whose uses do not exist.
6. When using the third-party code/API/libraries, always design your code such that these third-party things are easily replicable by others' code whenever we want.
7. Write unit tests of your code whenever possible (in real-world software development, it is too hard to maintain 100% code coverage by unit test due to the deadline and business).
8. When you write a unit test, keep the unit test also clean.
9. The success of software depends on some key elements. System design is a key element of them. So our system design should be clean and concise.
10. Using OOP design patterns whenever possible and where they are actually needed, because design patterns give us well-known and tested solutions to well-known problems.

### Final Word (miscellaneous)
***“Complexity kills. It sucks the life out of developers; it makes products difficult to plan, build, and test.”*** —Ray Ozzie, CTO, Microsoft Corporation.

So by the growth of software uses, system complexity also grows. New changes, features, and other stuff come and go regularly, so we need to handle all of the complexity as software engineers. Writing clean code makes handling complex tasks easy and smooth for others as well as ourselves.

---

*Insha Allah, in the upcoming parts, I will try to mention how we can write clean code, reason when our code becomes bad, and how can we remove our code smell. Until than, may Allah keep you healthy and happy.*