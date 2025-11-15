---
title: "Software Design Patterns and Principles - Part 12 (Command Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: "2025-11-15T00:00:00Z"
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "command-design-pattern"]
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
    image: "img/blogs/55-command.png"
    caption: "Command Design Pattern"
    alt: "Command Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 11:** [Software Design Patterns and Principles - Part 11 (Proxy Design Pattern)]({{< ref "blogs/54-proxy-design-pattern.md" >}})
- **Part 13:** [Software Design Patterns and Principles - Part 13 (Mediator Design Pattern)]({{< ref "blogs/56-mediator-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/55-command.png"
    caption="Command Design Pattern (Photo Credit: LearnCsDesign)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the command design pattern.

So let's get started...

---

## Story
{{< figure
    src="/img/blogs/55-command-story.png"
    caption="UML of Command Design Pattern (Photo Credit: Refactoring.guru)"
    align=center
>}}

The Refactoring Guru website gives very nice real-world analogies, like:

After a long walk through the city, you get to a nice restaurant and sit at the table by the window. A friendly waiter approaches you and quickly takes your order, writing it down on a piece of paper. The waiter goes to the kitchen and sticks the order on the wall. After a while, the order gets to the chef, who reads it and cooks the meal accordingly. The cook places the meal on a tray along with the order. The waiter discovers the tray, checks the order to make sure everything is as you wanted it, and brings everything to your table.

## Command Design Pattern
**Definition**:
> Command is a behavioral design pattern that turns a request into a stand-alone object that contains all information about the request. This transformation lets you pass requests as method arguments, delay or queue a request’s execution, and support undoable operations.

As the definition states, the command design pattern suggests a method as an object approach. It means turning a request into a stand-alone object. This stand-alone object can be executed anytime with delay, can be queued, and can be redone/undone as well.

**Problem**:

In the above story, you just place your choice, and the waiter just writes it down on paper. But how does a paper order turn into a real meal? How do different types of orders and different types of paper writings turn into meals after cooking?

The command design pattern is incredibly versatile and can be applied in various scenarios across different domains. Here are some common scenarios where the command design pattern can be used effectively:
- **GUI Applications**: Command patterns are frequently used in graphical user interface (GUI) applications, where user actions (such as button clicks or menu selections) need to be translated into commands. For example, each button in a GUI application can be associated with a specific command, allowing the application to execute different actions based on user input.
- **Remote Control Systems**: In systems where remote control functionality is required, such as home automation systems or TV remotes, the Command Pattern can be used to encapsulate and execute different commands remotely. Each button press on the remote can be mapped to a specific command object, allowing for easy customization and extension of functionality.
- **Transaction Management**: Command patterns are useful in scenarios where transactional operations need to be managed, such as database transactions. Each command represents a specific operation (e.g., insert, update, delete), and the Command Pattern can be used to encapsulate these operations and manage their execution within a transactional context.
- **Undo/Redo Functionality**: Command patterns are often employed to implement undo/redo functionality in applications. Each command encapsulates a specific action, and a history of executed commands is maintained. This allows users to undo (or redo) actions by reversing (or re-executing) the commands in the history.
- **Multi-level Menu Systems**: Command patterns can be used to implement multi-level menu systems, where each menu option corresponds to a specific command. This allows for hierarchical organization of menu options and simplifies the implementation of complex menu structures.
- **Batch Processing**: In applications that involve batch processing of tasks or jobs, the Command Pattern can be used to encapsulate individual tasks as command objects. These commands can then be executed sequentially or in parallel, depending on the requirements of the application.
- **Macro Recording and Playback**: Command patterns are useful for implementing macro recording and playback functionality in applications. Each user action is recorded as a command, and the recorded commands can be played back later to recreate the sequence of actions.
- **Asynchronous Task Execution**: In scenarios where asynchronous task execution is required, such as in web servers or distributed systems, the Command Pattern can be used to encapsulate asynchronous operations as command objects. This allows for decoupling of the initiation and execution of tasks, enabling more flexible and scalable architectures.

These are just a few examples of scenarios where the Command Design Pattern can be applied effectively. Its flexibility and versatility make it a valuable tool for designing modular, extensible, and maintainable software systems.

**Solution**:

In the above story, the paper order serves as a command. It remains in a queue until the chef is ready to serve it. The order contains all the relevant information required to cook the meal. It allows the chef to start cooking right away instead of running around clarifying the order details from you directly.

We can also use or implement the command pattern as a solution to the problems stated in earlier sections as well.

**UML Diagram**:
{{< figure
    src="/img/blogs/55-command-uml.png"
    caption="UML of Command Design Pattern (Photo Credit: Wikipedia)"
    align=center
>}}

Here in the UML diagram we can see that **Clients** interact basically with the **Invoker** class to invoke/execute the command. And all **ConcreteCommand** classes implement the **Command** interface. When the invoker invokes the command of one ConcreteCommand class, it then propagates the **Receiver** class **Action**().

**When To Use**:
- Use the Command pattern when you want to parametrize objects with operations.
- Use the Command pattern when you want to queue operations, schedule their execution, or execute them remotely.
- Use the Command pattern when you want to implement reversible operations.

**Implementation**:
```java
// Define the Command interface
interface Command {
    void execute();
}

// Concrete command classes
class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }
}

class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOff();
    }
}

// Receiver class
class Light {
    public void turnOn() {
        System.out.println("Light is on");
    }

    public void turnOff() {
        System.out.println("Light is off");
    }
}

// Invoker class
class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

// Client class
public class CommandPatternExample {
    public static void main(String[] args) {
        // Create the receiver
        Light light = new Light();

        // Create concrete command objects
        Command lightOnCommand = new LightOnCommand(light);
        Command lightOffCommand = new LightOffCommand(light);

        // Create invoker
        RemoteControl remote = new RemoteControl();

        // Associate commands with invoker
        remote.setCommand(lightOnCommand);
        remote.pressButton(); // Output: Light is on

        remote.setCommand(lightOffCommand);
        remote.pressButton(); // Output: Light is off
    }
}
```

Another C# implementation is available [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Behavioral%20Design%20Pattern/CommandDesignPattern/C%23).

---

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: Each command class encapsulates a single action or operation, adhering to the SRP. This promotes cleaner and more modular code, making it easier to understand, maintain, and extend.
- **Open/Closed Principle (OCP)**: The Command Pattern allows for the addition of new commands without modifying existing client code. Clients interact with commands through a common interface, enabling the system to be open for extension but closed for modification.
- **Encapsulation**: Commands encapsulate both the action to be performed and any necessary parameters or context required for that action. This encapsulation hides the details of how the action is carried out, promoting information hiding and reducing dependencies between components.
- **Separation of Concerns**: By encapsulating commands separately from their invokers (e.g., GUI elements, remote controls), the Command Pattern promotes a clear separation of concerns. This separation allows for more modular and reusable components, as changes to one component are less likely to affect others.
- **Decoupling**: The Command Pattern decouples the sender of a request from the receiver, allowing for more flexible and loosely coupled systems. Clients issuing commands do not need to know the details of how commands are executed, promoting a higher degree of abstraction and reducing dependencies.
- **Undo/Redo Functionality**: The Command Pattern facilitates the implementation of undo/redo functionality by storing command objects in a history list. This supports the principle of providing a mechanism to reverse operations, enhancing the user experience and increasing the robustness of the system.
- **Composite Pattern (if applicable)**: In some implementations, the Command Pattern can be combined with the Composite Pattern to create complex command hierarchies. This allows for the construction of composite commands that consist of multiple sub-commands, enabling the execution of compound operations.
- **Behavioral Design Patterns**: The Command Pattern is often used in conjunction with other behavioral design patterns, such as Observer, Memento, and Strategy. This allows for the implementation of more sophisticated interactions and behaviors within a system, promoting greater flexibility and adaptability.