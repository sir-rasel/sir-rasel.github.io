---
title: "Writing Clean Code - Part 4 (Identify Code Smells/Bad Code)"
description: "Let's learn how can we identify code smells or bad code"
date: 2025-08-21
tags: ["programming", "programming-basic", "clean-code", "code-smell", "bad-smell"]
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
    image: "img/blogs/14-code-smells.webp"
    caption: "Code Smells"
    alt: "Code Smells"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 3:** [Writing Clean Code - Part 3 (Formatting, Class & Object, Miscellaneous)]({{< ref "blogs/13-clean-code-bad-code-part-3-formatting-class-miscellaneous.md" >}})
---

{{< figure
    src="/img/blogs/14-code-smells.webp"
    caption="Code Smells (Photo Credit: Axify)"
    align=center
>}}

## Story
Our prophet Hazrat Muhammad Sallallahu Alayhi Sallam advised us that ***“Always try to avoid the acts of sin/bad things because if someone can avoid the bad work, he/she will start doing good work automatically.”*** 

This is true for both our real life and writing code. If we can avoid the code smell or bad code, then our code will automatically be good and clean. So identifying the code smell is important. 

Today I am trying to discuss some well-known code smells of code.

## Comments & Names
1. Comments with inappropriate information.
2. Obsolete comments. Comments that get old, irrelevant, and incorrect.
3. Redundant or unnecessary comment. Comment that does not hold enough relevance.
4. Comment out code. Code that is not in use and commented out.
5. Poorly written comment that leads someone in the wrong direction.
6. Choose undescriptive names.
7. Names that lead to implementation, not the correct level of abstraction.
8. Names that are ambiguous.
9. Names that are not self-described.
10. Encoded names that are not easily understandable.

## Functions & General Cases
1. Functions with too many arguments.
2. Functions with output arguments: generally, all programmers accept input as a function, so always try to avoid output parameters.
3. Boolean arguments loudly declare that the function does more than one thing. They are confusing and should be eliminated. So avoid the flag type as a function argument.
4. Dead function means functions that are no longer in use should be discarded.
5. Writing code in multiple languages in a single source file.
6. Obvious behaviors are unimplemented. It means a function or class doesn't implement its obvious behaviors that any programmers expect it to.
7. Incorrect behaviors for some corner cases, like boundary value. It means code that can’t pass the corner cases.
8. Code duplication. It means code that doesn’t follow the DRY (don’t repeat yourself) principle.
9. Too much information means classes or functions that are not small enough.
10. Dead code, meaning code that is no longer in use, should be discarded.

## Others
1. Inconsistency. It means mixing different styles of coding, formatting, naming conventions, etc.
2. Unused and messy codes, like variables, default constructors, test functions, etc., should be removed.
3. Code that obscures its intent. Means not expressive and understandable by others.
4. Misplaced responsibility or code. It indicates that code is not placed in the right file or right class.
5. Code that does not follow right, well, and team convention.
6. Negative conditionals mean checking logical NOT (!) conditions. It should be avoided as much as possible.
7. Inherit constants and static value.8. Use int or another static type rather than enum for the flag value.

#### And Finally, avoid anything that your team think is not right.