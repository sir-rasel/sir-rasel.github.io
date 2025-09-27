---
title: "Java Crash Course - Part 1 (Before Start)"
description: "Let's learn writing program with Java"
date: 2025-09-26
tags: ["programming", "language", "java", "crash-course"]
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
    image: "img/blogs/30-java-language.webp"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Java Crash Course - Part 2 (Fundamental Basics)]({{< ref "blogs/31-java-part-2-fundamental-basics.md" >}})
---

{{< figure
    src="/img/blogs/30-java-language.webp"
    caption="Java Programming Language (Photo Credit: Orient Software)"
    align=center
>}}

## What Is Java and Its Brief History
Java is a programming language that is used to write computer programs. It is an object-oriented programming (OOP) language, which means it supports all the OOP concepts. Its syntax is a lot similar to the other popular languages like C, C++, and C#.

Java was developed at Sun Microsystems (which is now a subsidiary of Oracle) in the year 1995 by James Gosling and his team. At first its name was Oak, and then it changed to Java. The most important thing about Java is that a program written in Java is platform independent, which means it can run on any platform, whatever it is—Windows, Linux, or Mac.

## Java Platforms / Editions
There are 4 platforms or editions of Java:

***1. Java SE (Java Standard Edition)***
- It is a Java programming platform. It includes Java programming APIs such as java.lang, java.io, java.net, java.util, java.sql, java.math, etc. It includes core topics like OOPs, String, Regex, Exception, Inner Classes, Multithreading, I/O Stream, Networking, AWT, Swing, Reflection, Collection, etc.

***2. Java EE (Java Enterprise Edition)***
- It is an enterprise platform that is mainly used to develop web and enterprise applications. It is built on top of the Java SE platform. It includes topics like Servlet, JSP, Web Services, EJB, JPA, etc.

***3. Java ME (Java Micro Edition)***
- It is a micro platform that is dedicated to mobile applications.

***4. JavaFX***
- It is used to develop rich internet applications. It uses a lightweight user interface API.

When anyone talked about only Java, basically they were referring to the standard edition (SE). And Java SE is the base of all others. On this day of writing this blog, recently released Java 25 is the latest LTS version available.

## Types of Java Applications
Almost every type of application can be built using Java. Some of them are:
- Desktop application
- Web application
- Enterprise application
- Mobile application
- Embedded System etc.

## Features
{{< figure
    src="/img/blogs/30-java-features.jpeg"
    caption="Java Features (Photo Credit: javaTpoint)"
    align=center
>}}

- Simple
- Object Oriented
- Portable
- Platform Independent
- Secured
- Robust
- Architecture neutral
- Interpreted
- High Performance
- Multithreaded
- Distributed
- Dynamic

## Executional Process of Java Program
{{< figure
    src="/img/blogs/30-java-execution.jpeg"
    caption="Java Program Execution Process (Photo Credit: javaTpoint)"
    align=center
>}}

Java program execution is being done in 2 phases: 
1. Compile Time
2. Run Time

And follows the below steps:
- **Step 1:** Write code in Java.
- **Step 2:** Compile the Java code, and then the compiler starts checking for errors like syntax, compilation, runtime, memory overflow, etc. If compilation becomes successful, then it generates *.class* files.
- **Step 3:** Convert the code into *bytecode* (.class files collection).
- **Step 4:** Load the bytecode into the Java Virtual Machine (*JVM*).
- **Step 5:** Convert the bytecode into *machine code* using the JVM, and this process is complex in 3 easy steps -->> class loader, bytecode verifier, and just-in-time compilation (*JIT*).
- **Step 6:** After step 5, our code compiles to a machine code called *binary* executables.

## Important Java Terminology
- ***Java Development Kit (JDK):*** The JDK is a software development environment that provides the tools and libraries necessary for developing and running Java applications. The JDK includes the Java Runtime Environment (JRE), which is necessary for running Java applications, as well as development tools such as the Java compiler (javac), the Java Archive tool (jar), and the Java debugger (jdb).

- ***Java Virtual Machine (JVM):*** It is an abstract machine that provides a consistent runtime environment for Java programs to execute while also providing important features such as memory management, garbage collection, and a security model that helps protect Java programs from malicious code.

- ***Java Runtime Environment (JRE):*** It is a software package that provides the minimum set of tools and libraries required to run Java applications, including the JVM and a set of core libraries and APIs. It is designed for end-users who only need to run Java applications and is typically included as part of the installation package for Java applications.

- ***Byte Code:*** It is the compiled form of Java source code that is executed by the Java Virtual Machine (JVM). It is a highly optimized set of instructions that can be executed on any platform that has a compatible JVM installed, making Java a platform-independent programming language.

---

*Insha Allah, in the upcoming part, I will try to share the fundamental basics of Java. Until than, may Allah keep you healthy and happy.*