---
title: "Writing Clean Code - Part 2 (Name, Function, Comment)"
description: "Let's learn how can we write meaningful name, function and comment"
date: 2025-08-19
tags: ["programming", "programming-basic", "clean-code", "code-smell", "bad-smell", "meaningful-name", "function", "comment"]
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
    image: "img/blogs/12-clean-code-name-function-comment.JPG"
    caption: "clean code"
    alt: "clean code"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Writing Clean Code - Part 1 (Conceptually Clean and Bad Code)]({{< ref "blogs/11-clean-code-bad-code-part-1-concept.md" >}})
---

{{< figure
    src="/img/blogs/12-clean-code-name-function-comment.JPG"
    caption="Clean Code - Name, Function, Comment (Photo Credit: Prezi)"
    align=center
>}}

Remember 2 things:
1. The only measurement of your code is WTFs / Minute. That is what the readers feel when reviewing code.
2. Linux Torvalds, the creator of the Linux operating system, says, ***“Talk is cheap; show me the code.”***

So if we connect the above 2 points, then we can easily understand that our code should be talkable and self-describing because when anyone reviews/reads our code, they should feel well and comfortable enough. 

In this section we are talking about the ways we can write clean code and avoid the badness/WTFs of our code.

## Meaningful Names
In the real world, a name carries the identity of something. A name describes what a thing is, why it is, what type of work it does, etc. That means a name indicates the metadata of something. Like the real world, when coding names of anything, it can be a variable, function, class, etc., and should carry its identity and meaning. 

Below are some useful tips for meaningful names, and by maintaining those tips, we can keep our code clean in terms of naming:

1. Use intention-revealing names.
2. Use self-describing names, not comments, to describe it.
3. Avoid disinformation; avoid names that are misleading.
4. Make meaningful distinctions; avoid misspelling.
5. Use pronounceable names.
6. Use searchable names.
7. Avoid encoding.
8. Avoid mental mapping, because your mental mapping is not known to others.
9. Class and variable names should be nouns.
10. The method name should be a verb.
11. Don’t be cute when naming, like cutey, sweety, gulu gulu, etc.
12. Pick one word per concept.
13. Avoid the same word for multiple purposes.
14. Use solution domain names.
15. Use problem domain names.
16. Add meaningful context.
17. Don’t add gratuitous context.
18. Keep the name short by obeying all other rules.

### Final Word (meaningful names):
***"There are only two hard things in computer science: cache invalidation and naming things."*** – Phil KarltonSo.

It is easily understandable that choosing the right and meaningful names is not as easy a task as it seems. Programmers need a good descriptive skill for it. It comes from experience and obeying the tips/rules year after year. So start practicing good names and keep your code clean.

## Functions
We use functions in our day-to-day life or coding. A function helps us to modularize our code and increase the reusability of our code. So our function should be clean enough for others. 

Below are some tips for writing clean functions:

1. First of all, a function should be functional at its work.
2. A good, descriptive, meaningful name, possibly with a verb prefix.
3. Small in size, ideally 3-30 lines.
4. Maintain proper indentation.
5. Avoid nested blocks; try to keep in single blocks.
6. Do one and only one thing.
7. One level of abstraction per function; avoid mixing multi-level abstraction.
8. Maintain the step-down rule, which means writing functions in a top-to-bottom hierarchy.
9. The number of arguments should be as minimum as possible. Possibly zero; more arguments indicate more responsibility of a function.
10. Try to avoid flags as function arguments, because it makes branching and violates the single responsibility of a function.
11. A good function should have no side effects; it should be identical.
12. Functions should avoid output parameters or pass by reference as much as possible.
13. Prefer exception to return exceptions.
14. Extract try-catch blocks using functions.
15. Follow the DRY (don't repeat yourself) principle; you should not write the same code multiple times. That's why we use functions.
16. Functions should either do something or answer something, but not both.

### Final Word (functions)
***Functions should do one thing. They should do it well. They should do it only.*** – Clean Code Book.

By keeping your function clean and small, you can reuse the functionality over the codebase, and it will be much easier for other programmers/developers to understand the philosophy behind the function.

## Comments
I am sure many of us have heard that more commenting in our code is good. But the truth is comments are bad for code too often. Comments are considered the compensation for our failure to express the theme that we can’t express using our code. So comment your code where it is actually needed, and it should be good enough.

Below are some tips for writing clean comments:

1. Do not comment to make up for the bad code. It means don’t comment because your code is bad and you need to explain it using comments. 
2. Always try to express yourself by code, not using comments.
3. Comments on legal things like copyright and authorship statements.
4. Comments for giving the basic information, like the parameter type it takes and the return type.
5. Comments for explaining the intent.
6. Sometimes the clarification of some obscure statements is good.
7. Sometimes comments warning of the consequences are useful.
8. Giving ToDo comments is not bad at all.
9. Amplifying the important purpose by comments is good.
10. Avoid redundant comments.
11. Do not write comments larger than the code itself.
12. Inaccurate comments are far worse than no comments at all.
13. Avoid misleading comments.
14. Update the comments when you update your code; otherwise, it will be evil one day.
15. Avoid noisy comments, comments that are for nothing.
16. Avoid closing braces in comments; it's unnecessary at all.
17. Don’t use comments when you can use functions or variables.
18. Strongly avoid keeping commented-out code because in the near future it will be a headache for you.
19. Avoid large comments for giving too much information.

### Final Word (comments)
***“Don’t just comment on bad code, rewrite it.”*** - Brian W. Kernighan and P. J. Plaugher.

Comments are useful when they're meant to be. But code that can express its intent itself without comment is more prestigious and clean. So always avoid bad comments and start practicing good comments. But more importantly, start writing code that is self-describing without comment.

---

*Insha Allah, in the upcoming parts, I will try to mention how we can write clean code, reason when our code becomes bad, and how can we remove our code smell. Until than, may Allah keep you healthy and happy.*