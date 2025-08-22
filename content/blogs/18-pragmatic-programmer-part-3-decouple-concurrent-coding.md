---
<<<<<<< HEAD
title: "Becoming a Pragmatic (Better) Programmer - Part 3 (Decouple, Concurrent Coding, Project & Team)"
=======
title: "Becoming a Pragmatic (Better) Programmer - Part 3 (Decouple, Concurrent, Coding)"
>>>>>>> 2ae32ea (Add 18th post)
description: "Tips for becoming or improving as a better programmer"
date: 2025-08-25
tags: ["programming", "coding", "pragmatic-programmer", "decouple-concurrent-coding"]
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
    image: "img/blogs/18-pragmatic-code.png"
    caption: "Pragmatic Programmer"
    alt: "Pragmatic Programmer"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Becoming a Pragmatic (Better) Programmer - Part 2 (Design, Implement, Debug)]({{< ref "blogs/17-pragmatic-programmer-part-2-code-debug.md" >}})
---

{{< figure
    src="/img/blogs/18-pragmatic-code.png"
    caption="Pragmatic Programmer (Photo Credit: Unsplash)"
    align=center
>}}

## Story
Remember the guy Ismael from the previous part? He was good at broad-level thinking while coding and efficiently designing software. Today he shares some tips and tricks for making code decoupled and concurrent.

### Decouple and Concurrent Coding Tips
- Maintain SRP (single responsibility principle) and reduce inter-component dependency, because decoupled code is easier to change.
- Depend on internal state, not external, which means call some component, and this will tell something. But don't ask external components for internal decision-making.
- Don't chain method calls to do something; instead, create a pipeline based on data.
- Avoid global data; if it's extremely important, then wrap global data into an API.
- Use well-designed patterns and programming paradigms according to business needs.
- Don't pay inheritance tax, which means avoid inheritance as much as possible. Use interfaces to achieve polymorphism.
- Prefer composition over inheritance, meaning create Has-A relationships, not Is-A, whenever possible.
- Frequently changed values should be parameterized using an external configuration service.
- Analyze workflow to improve concurrency.
- Use an activity diagram for better understanding of concurrent workflow.
- Be very aware of the shared states, and remember random failures are often concurrency issues.
- Use blackboards and pen and paper for high-level analysis of workflow.

---

## Story
Osama is an experienced software developer currently playing the team lead role. But despite being a team lead, he is actively coding regularly. Because he loves coding. He has a very good track record of following good coding practices and is also known as a "pro-coder" in his colleagues' circle.

### Remember While Coding
- Maintain clean code rules like good naming conventions, maintain consistency, use small and good functions, etc.
- Use appropriate design patterns where applicable.
- ***"While coding, listen to your inner lizard"*** means if you feel there is something wrong, then of course there is something wrong. Try to find it and spot-fix it.
- When you spot things done in a way that seems strange, jot it down and try to explore later.
- Don't program by coincidence. It means don't code based on assumption; prove it first.
- While working with date and time, please prefer UTC format rather than local format.
- Always be aware of what you are doing and try to explain it to your junior. If you can't explain well, then there is a gap in your own understanding. 
- Use the optimized and fastest algorithm and estimate your code complexity. That will give you better understanding and confidence in your solution.
- Refactor old, legacy bad code in a routine and regular basis. Don't just keep the broken window day after day.
- Always write test codes, because without test codes your code should not becomplete.
- Build end-to-end testing, not top-down or bottom-up.
- Always be concerned about security, and follow the basic security principles. Apply any security patches as early as possible.

--- 

### Build Pragmatic Projects & Pragmatic Team
- About the project requirements, remember one thing: "No one knows exactly what they want."
- Programmers are the ones who help people to understand what they want.
- Start project prototyping and getting exact requirements in a feedback loop.
- Work with a user to think like a user.
- Try to separate the requirements and policy and consider policy as metadata because they are being frequently changed over time.
- Use a project glossary to specify the keywords related to the project knowledge data.
- When working on clients' projects, "Don't think outside the box, but always find the right box."
- A pragmatic team is a team that is small in size and stable in terms of retention.
- Members of a pragmatic team are also pragmatic individually.
- Team members are always talking to each other as much as possible.
- They are always sharing their knowledge with each other.
- Do what works, not what's fashionable, and deliver that when the user needs it.
