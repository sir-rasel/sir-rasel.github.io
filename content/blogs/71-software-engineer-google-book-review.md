---
title: "Book Review and Insights Learning: (Software Engineering at Google)"
description: "Let's learn the software engineering differently!"
date: "2025-12-03"
tags: ["software-engineering-at-google-book", "book-review"]
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
    image: "img/blogs/71-engineering-google-book.png"
    caption: "Software Engineering At Google"
    alt: "Software Engineering At Google"
    relative: true
    hidden: true
---

---
### Detailed Software Engineering Series:
- **Part 1:** [All About Software Engineering: Part 1 (Science, Engineering and Mindset Part)]({{< ref "blogs/63-software-engineering-science.md" >}})
---

{{< figure
    src="/img/blogs/71-engineering-google-book.png"
    caption="Software Engineering at Google Book (Photo Credit: Software Engineering Daily)"
    align=center
>}}

## Book introduction
"**Software Engineering at Google: Lessons Learned from Programming Over Time**" Curated by Titus Winters, Tom Manshrech & Hyrum Wright, Software Engineering at Google is a book that encapsulates the collective knowledge and practices of software engineering as experienced by Google. The book aims to provide insights into the strategies, tools, and cultural practices that have contributed to Google's success in building and maintaining some of the world's most complex and scalable software systems.

It was first published in March 2020, and after that, it gained huge popularity among the software engineering community. This book reflects the software engineering process at Google so nicely.

## About Author
**Titus Winters** is a Senior Staff Software Engineer at Google, where he has worked since 2010. Today, he is the chair of the global subcommittee for the design of the C++ standard library. At Google, he is the library lead for Google’s C++ codebase: 250 million lines of code that will be edited by 12K distinct engineers in a month. 

**Tom Manshreck** is a Staff Technical Writer within Software Engineering at Google since 2005, responsible for developing and maintaining many of Google’s core programming guides in infrastructure and language. Since 2011, he has been a member of Google’s C++ Library Team, developing Google’s C++ documentation set, launching (with Titus Winters) Google’s C++ training classes, and documenting Abseil, Google’s open source C++ code. 

**Hyrum K. Wright** is a Staff Software Engineer at Google, where he has worked since 2012, mainly in the area of large-scale maintenance of Google’s C++ codebase. Hyrum has made more individual edits to Google’s codebase than any other engineer in the history of the company.

## High-level Overview
The book emphasizes three fundamental principles that we feel software organizations should keep in mind when designing, architecting, and writing their code: 
- **Time and Change**, or how code will need to adapt over the length of its life 
- **Scale and Growth**, or how an organization will need to adapt as it evolves 
- **Trade-Offs and Costs**, or how an organization makes decisions, based on the lessons of Time and Change and Scale and Growth

The book is structured to cover a wide range of topics, from high-level engineering principles to specific technical implementations. Each chapter is designed to be self-contained, allowing readers to focus on particular areas of interest. Case studies and examples from Google's projects are used to illustrate key points and provide practical insights.

---

## Insights and Learning
- Programming is about just coding for a short term; on the other hand, software engineering is about managing complexity, making systems maintainable, and focusing on long-term success rather than short-term fixes.
- The 3 fundamental things we should consider when performing software engineering are time and change, scale and growth, and tradeoff and costs. To tackle this, we need to determine the company's and team's: Culture, Processes, Tools.
- In software engineering, there is no one-size-fits-all solution. We always need to take the best-suited tradeoff decision based on the situation.
- Always remember we should prefer "it works" over "it is maintainable" when doing software engineering.
- Hyrum's law: "With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody."
- Avoid assumption-based programming, meaning don't think nothing will change; think there is always a possibility for change.
- No matter how big or small your system is today, please always think and keep the scalability in consideration.
- Remember, the term "shifting left" means always catching and solving any issue as early in the SDLC as possible.
- Be data driven and experimental. Not doing something based on "Do it as I said so."
- Emphasizes communication, empathy, code reviews, and shared ownership to build high-functioning teams.
- Share something with the team without fear and insecurity.
- Fail early, fail fast, fail often, and reduce the bus factor.
- The 5 pillars for a good team are humility, respect, trust, collaboration, and empathy.
- Encourages documentation, mentoring, and the use of internal tools for knowledge dissemination.
- Avoid single points of failure.
- Keep learning and grow your knowledge base by reading, exploring, asking questions, etc.
- Cultivate a knowledge-sharing culture by tech talks or tech adda.
- Advocates for proactive measures to promote diversity and equity within engineering teams.
- When designing and developing a product, please consider the motto "Build for/with everyone."
- Highlights the importance of setting clear goals, providing support, and fostering a culture of trust.
- Cultivate a skill called "influence without authority."
- If you are a leader/manager, then don't ignore low performers and human issues, and don't compromise the hiring bar.
- If you are a leader/manager, then be a mentor, lose ego, remove team roadblocks, be honest, and track team happiness.
- Delegate where possible; don't do it yourself. The mission should be to build the self-driving team.
- The cycle of success is analysis, struggle, traction, and reward.
- Productivity metrics should align with overall goals and team health. It should be a mix of qualitative and quantitative metrics.
- Use the GSM (Goals, Signals, Metrics) framework to calculate productivity.
- Create rules, apply rules, and automate enforcement of rules when possible for maintaining consistency.
- Establishes best practices for effective code reviews, emphasizing feedback and collaboration. Establish automation for early-stage review.
- The universal truth is: Code is a liability, but functionality or the product of code is the asset.
- Advocates for writing clear, concise, and up-to-date documentation for all aspects of the codebase. Documentation should be treated like code.
- Documentation should be for others/audiences, not for yourself.
- Documentation should address the who, what, when, where, and why aspects.
- Documentation should follow a well-organized beginning, middle, and end format.
- Encourages a robust testing strategy, including unit, integration, and end-to-end tests. Testing ensures reliability and quality.
- Test scope and test size should be as small as possible.
- Code with test coverage is something that supports frequent change with confidence.
- Automated test runs with scale are the key and need time to adopt.
- Test behaviors, not methods.
- Proper use of test doubles (mocks, stubs, etc.) can make tests more reliable and easier to write.
- Integration testing checks the interactions between components. Suggests focusing on critical paths and using automation to manage complexity.
- Balancing test coverage and performance is key. Recommends a layered approach to testing to balance thoroughness and efficiency.
- Deprecation is something that needs extra care. Only an alert is not enough; somebody needs to take care of the proper migration from deprecated code implicitly.
- Always use a version control system (VCS) and minimize the source of truth (possibly keep one version).
- Use and master regularly used IDEs, like code search, bulk change, shortcuts, etc., for boosting development.
- Use tools for better outcomes and increased productivity, like automated code review tools and static analysis tools for catching early bugs/issues.
- Give extra care for dependency (can be library, package, or 3rd party API) management (both internal and external). Prefer the SemVer model to do that.
- Incrementally update the dependent package/library regularly. And prefer the minimum version update (meaning minimum jump while updating).
- LSC (large-scale change) needs extra care and should be done with caution. Always make sure proper testing is done after LSC performs.
- Velocity is a team sport; faster is safer. So develop and practice a good CI/CD (Continuous Integration/Continuous Delivery) process with proper tools.
- For better user experience and product success, we need automated monitoring and resource management based on need. So SRE practice is a must to ensure auto-scaling and growth.

## Conclusion
Overall, the book serves as both a practical guide and a source of inspiration for anyone involved in software engineering. By sharing the lessons learned from Google’s extensive experience, it aims to contribute to the advancement of software engineering practices across the industry.

Every software professional no matters he/she is an engineer, an manager, team lead, product should read this book at least once. That will give a solid understanding about the software and its engineering.