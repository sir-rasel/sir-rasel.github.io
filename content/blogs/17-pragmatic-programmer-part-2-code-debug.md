---
title: "Becoming a Pragmatic (Better) Programmer - Part 2 (Design, Implement, Debug)"
description: "Tips for becoming or improving as a better programmer"
date: 2025-08-24
tags: ["programming", "coding", "pragmatic-programmer", "designing-coding-debugging"]
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
    image: "img/blogs/17-pragmatic-implement.png"
    caption: "Pragmatic Programmer"
    alt: "Pragmatic Programmer"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Becoming a Pragmatic (Better) Programmer - Part 1 (Intro, Team Player)]({{< ref "blogs/16-pragmatic-programmer-part-1-team-player.md" >}})
- **Part 3:** [Becoming a Pragmatic (Better) Programmer - Part 3 (Decouple, Concurrent Coding, Project & Team)]({{< ref "blogs/18-pragmatic-programmer-part-3-decouple-concurrent-coding.md" >}})
---

{{< figure
    src="/img/blogs/17-pragmatic-implement.png"
    caption="Pragmatic Programmer (Photo Credit: Unsplash)"
    align=center
>}}

## Story
Ismael gets hired by an established IT company as a senior software developer. He has worked on several projects and in various business fields throughout the years, gaining expertise and experience. Based on his skills and experience, he keeps a respectable approach when designing or programming a system.

He creates systems that are easy to alter and adhere to the ETC (easier to change). When programming or generating anything similar (such as documentation, an API standard, or something else), follow the DRY (don't repeat yourself) guidelines. Create reusable code or components to be used again. He consistently tries to uphold the SRP (single responsibility principle) and prevent interactions between unrelated items, which is a crucial aspect.

He tries to create systems that are independent of one another and are easily reversible in the event of a disaster. Another crucial habit he upholds is his constant awareness in regard to estimating. Before concluding anything, he does a POC (proof of concept) and uses the prototyping technique to demonstrate it in an early stage. Even if the prototype doesn't have to be perfect, he tries to make it as good as possible so that it may be reused when the POC is approved and the full project has to be put into action.

### Software Design and Coding Tips
- Always remember, the only constant thing in software engineering is change. So always be ready to adopt change.
- Good design is easier to change than bad design, so learn and practice good design and ETC design.
- Practice to maintain the DRY principle, which means while coding, documenting, or doing something else, keep it single and don't repeat yourself.
- Design a class or service by maintaining SRP (single responsibility principle). 
- Maintaining orthogonality means designing and coding software with decoupled components and eliminating effects between unrelated components.
- Write testable code and design a well-tested system.
- While coding and designing system components, always keep reversibility in mind in case of any disaster.
- Learn to create good POC (proof of concept) and prototyping. And while prototyping something, keep it compact so that it can be used when the full project has to be put into action.
- Learn estimating by breaking down large systems into small components and writing code by reflecting closely on domain knowledge.

---

## Story
Zahir and Omar are colleagues and work in a software development company. Zahir is an experienced developer, and Omar just started his career in this field. With the years of experience, Zahir developed some habits that keep him active and productive. Like keeping notes or tracking knowledge, using tools like IDE efficiently, writing shell scripts to automate repetitive tasks, using a version control system, and planning each day and scheduling it.

On the other hand, Omar does not pretty much do these things. Still, he is trying and learning these habits. Another thing is, he gets panic when a bug lands and does not take the same approach as what Zahir does. But Omar is a quick learner, and day by day he is gaining the knowledge and experience.

### Tools and Debugging Tips
***Tools:***
- Keep knowledge and notes in plain text regularly.
- Use the power of command shell and scripting.
- Automate commands and configure aliases for regularly used commands as you like.
- Automate regular repetitive tasks and write scripts for them.
- Use tools that are easy to use and increase your productivity.
- Achieve fluency in the editor or IDE that you regularly use.
- Always use version control whatever the work size is.

***Debugging:***
- Don't panic; be calm.
- Fixed the problem, not the blame.
- Use logging and try to regenerate the bug locally.
- Don't just assume the problem; prove it and fix it.
- Don't try to avoid the problem sneakily; let it crash early. Because an early crash does less damage than a crippling one.

---

*Insha Allah, in the upcoming parts, I will try to share more tips to address others area. Until than, may Allah keep you healthy and happy.*