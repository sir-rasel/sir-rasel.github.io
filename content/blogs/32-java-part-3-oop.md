---
title: "Java Crash Course - Part 3 (Object Oriented Programming)"
description: "Let's learn writing program with Java"
date: 2025-09-28
tags: ["programming", "language", "java", "crash-course", "oop", "object-oriented-programming", "class-object"]
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
    image: "img/blogs/30-java-oop.png"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Java Crash Course - Part 2 (Fundamental Basics)]({{< ref "blogs/31-java-part-2-fundamental-basics.md" >}})
- **Part 4:** [Java Crash Course - Part 4 (Miscellaneous)]({{< ref "blogs/33-java-part-4-miscellaneous.md" >}})
---

{{< figure
    src="/img/blogs/32-java-oop.png"
    caption="Java Object Oriented Programming (Photo Credit: Raygun Blog)"
    align=center
>}}

***N.B:*** Please read the following concepts for better understanding before continue reading this article.

☛ [Common Programming Style]({{< ref "blogs/5-lets-feel-programming-part-5-programming-style.md" >}})

---

## Story
Once upon a time, there was a village where people lived in simple houses made of mud and straw. One day, a group of architects arrived in the village with plans to build new houses made of bricks and cement.

The architects knew that they needed to create a set of blueprints to guide the construction of the new houses. They decided to use an object-oriented approach to design the blueprints, which would allow them to represent the houses as a set of interconnected objects with properties and behaviors.

First, the architects identified the different parts of the house, such as the walls, roof, doors, and windows. Each of these parts was represented as an object, with its own set of properties and behaviors. For example, the walls object had properties such as height, width, and color, and behaviors such as the ability to be painted or repaired.

Next, the architects used the concept of inheritance to create specialized objects based on the original objects. For example, they created a door object that inherited properties and behaviors from the wall object, but also had its own unique properties such as a handle and lock. They create some frame which helps to create other objects but the frame it self is abstract means those can not use directly for building house.

The architects also used the concept of encapsulation to hide the implementation details of the objects from the outside world. They created interfaces that allowed the houses to be constructed and maintained without exposing the internal workings of the objects.

Finally, the architects used the concept of polymorphism to create objects that could take on multiple forms. For example, they created a window object that could be either a single pane or a double pane, depending on the needs of the house.

Thanks to the object-oriented approach used by the architects, the construction of the new houses was a great success. The houses were sturdy, functional, and easy to maintain, and the villagers were delighted with their new homes. And so, the architects returned to their own village, knowing that their use of object-oriented programming had made a real difference in the lives of others.

{{< figure
    src="/img/blogs/32-java-oop-pillar.png"
    caption="Java Object Oriented Programming (Photo Credit: javaTpoint)"
    align=center
>}}

## The Pillars of Object Oriented Programming
1. **Class:** It can also be defined as a blueprint from which you can create an individual object. Class doesn't consume any space. In the above story the architects set of blueprints are nothing but class.

2. **Object:** Any entity that has state and behavior is known as an object. It can be defined as an instance of a class. An object contains an address and takes up some space in memory. In the above story house, wall, door etc. are the example of object.

3. **Encapsulation:** Encapsulation is the process of hiding the implementation details of an object from the outside world and restricting access to them through a well-defined interface. This helps to protect the integrity of the object's data and prevent external interference. In the above story hiding the house building process details can be an example of encapsulation.

4. **Inheritance:** Inheritance is the mechanism by which a class can inherit properties and behaviors from another class. Inheritance allows for the reuse of code and the creation of specialized classes that can add or override the behavior of their parent class. In the above story wall object give door objects behavior is an example of inheritance. 

5. **Polymorphism:** Polymorphism is the ability of an object to take on multiple forms. In Java, this is typically achieved through method overloading and method overriding. Polymorphism allows for the creation of code that can work with objects of multiple types, and can help to make code more flexible and adaptable. In the above story window objects multiple behavior can be an example of polymorphism.

6. **Abstraction:** Abstraction is the process of representing complex real-world objects in a simplified way. In Java, this is typically achieved through the use of abstract classes and interfaces. Abstraction allows for the creation of code that can be easily maintained and extended, as changes to the implementation of an object can be made without affecting the rest of the code that uses it. In the above example frame for making objects can be an example of abstraction. In java abstract class can not create an object like the frame of the story.

### Conceptual Implementation:
Please note that, this is just a conceptual implementation.
```java
// Parent class representing a generic house
class House {
    private String color;
    private int height;
    private int width;
    
    public House(String color, int height, int width) {
        this.color = color;
        this.height = height;
        this.width = width;
    }
    
    public String getColor() {
        return color;
    }
    
    public void setColor(String color) {
        this.color = color;
    }
    
    public int getHeight() {
        return height;
    }
    
    public void setHeight(int height) {
        this.height = height;
    }
    
    public int getWidth() {
        return width;
    }
    
    public void setWidth(int width) {
        this.width = width;
    }
    
    public void paint(String color) {
        setColor(color);
        System.out.println("The house has been painted " + color + ".");
    }
    
    public void repair() {
        System.out.println("The house has been repaired.");
    }
}


// Child class representing a door object that inherits properties and behaviors from the House class
class Door extends House {
    private String handle;
    private String lock;
    
    public Door(String color, int height, int width, String handle, String lock) {
        super(color, height, width);
        this.handle = handle;
        this.lock = lock;
    }
    
    public String getHandle() {
        return handle;
    }
    
    public void setHandle(String handle) {
        this.handle = handle;
    }
    
    public String getLock() {
        return lock;
    }
    
    public void setLock(String lock) {
        this.lock = lock;
    }
    
    public void open() {
        System.out.println("The door has been opened.");
    }
    
    public void close() {
        System.out.println("The door has been closed.");
    }
}


// An interface representing the construction and maintenance of houses
interface HouseBuilder {
    public House buildHouse(String color, int height, int width);
    public void paintHouse(House house, String color);
    public void repairHouse(House house);
}


// A class implementing the HouseBuilder interface
class HouseBuilderImpl implements HouseBuilder {
    public House buildHouse(String color, int height, int width) {
        return new House(color, height, width);
    }
    
    public void paintHouse(House house, String color) {
        house.paint(color);
    }
    
    public void repairHouse(House house) {
        house.repair();
    }
}


// Main class for testing the HouseBuilder implementation
public class HouseDemo {
    public static void main(String[] args) {
        HouseBuilder houseBuilder = new HouseBuilderImpl();
        
        // Build and paint a new house
        House house = houseBuilder.buildHouse("blue", 10, 20);
        houseBuilder.paintHouse(house, "green");
        
        // Build and repair a door on the house
        Door door = new Door("green", 7, 3, "silver", "deadbolt");
        houseBuilder.repairHouse(door);
        door.open();
        door.close();
    }
}
```
---

*Insha Allah, in the upcoming part, I will try to share the Thread Programming of Java. Until than, may Allah keep you healthy and happy.*