---
title: "Software Design Patterns and Principles - Part 6 (Builder Design Pattern)"
description: "Let's learn the software and OOP design patterns and principles!"
date: 2025-11-05
tags: ["design-pattern", "design-principle", "oop-design-pattern", "oop-design-principle", "software-design-pattern", "builder-design-pattern"]
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
    image: "img/blogs/49-builder.png"
    caption: "Builder Design Pattern"
    alt: "Builder Design Pattern"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 5:** [Software Design Patterns and Principles - Part 5 (Factory Method and Abstract Factory Method Design Pattern)]({{< ref "blogs/48-factory-and-abstract-factory-design-pattern.md" >}})
- **Part 7:** [Software Design Patterns and Principles - Part 7 (Adapter Design Pattern)]({{< ref "blogs/50-adapter-design-pattern.md" >}})
---

{{< figure
    src="/img/blogs/49-builder.png"
    caption="Builder Design Pattern (Photo Credit: Dev Genius)"
    align=center
>}}

In this series, we try to explore software design patterns and principles. We will try to learn the well-known OOP design patterns one by one. In this part, we try to explore the builder design pattern.

So let's get started...

---

## Story
My friend Bablu starts a house construction company. At the beginning of his company, he only offers a small set of features and options for building houses for his customers. For example, offers to choose the number of rooms, number of windows, and number of washrooms and kitchens. Also, he creates software that accepts customer choices based on available options that Bablu offers. But day by day his company becomes famous and large. And customers want more and more options, features, and flexibility for building their dream house. Now Bablu offers a number of south-facing windows, doors, floor colors, ceiling colors, etc., and that's why he needs to adopt the options and feature choice variety in his created software.

## Builder Design Pattern
**Definition**:
> Builder is a creational design pattern that lets you construct complex objects step by step. It allows you to produce different types and representations of an object using the same construction code.

As the definition states, the builder pattern helps us build a complex object step by step. It means an object that has a complex creation mechanism and too many options and representations. An object that can be different types and representations based on the creational choice/logic. So in this scenario, the builder pattern gives us a central construction coding mechanism that can be used to create different types and representations of the object.

**Problem**:

In the above story, at the beginning of Babul's construction company, his software has a class named Home. And this class has only the following properties: numberOfRoom, numberOfWindow, numberOfWashroom, and numberOfKitchen. So to make this **Home** class object, the class can easily contain a constructor like **Home (numberOfRoom, numberOfWindow, numberOfWashroom, numberOfKitchen)**;

But what about the next phase where many more properties are being added and every customer doesn't choose every property? That's why here increasing property and initializing them using a constructor is ugly and hard.

So how can we adopt the current and future changes cleanly and easily and create objects by initializing them with proper property values?

**Solution**:

From the above definition of the builder pattern, it gives us an object construction mechanism for different types and representations of the same object. So the builder pattern is one of the solutions to our described problem. What we need is just to separate the object construction code and make an interface for the common property initialize/setter methods. Let's call it **HouseBuilder**. Then create a concrete house builder class called **ConcreteHouseBuilder** by implementing the HouseBuilder interface. We can also create a **ConcreteDuplexHouseBuilder** class for building duplex houses. Then we need to define the product, meaning the house class that will be created/built as the final result. We also need a Director class, which will accept the customer choice/logic and handle the steps of object initialization/creation.

**UML Diagram**:
{{< figure
    src="/img/blogs/49-builder-uml.jpeg"
    caption="UML of Builder Design Pattern (Photo Credit: Google)"
    align=center
>}}

Here in the UML diagram, we see that the Builder interface declares product construction steps that are common for all types of builders. **ConcreteBuilder** implements the Builder interface and provides implementations of construction steps. **Products** are the resulting objects that are built by ConcreteBuilder. The **Director** class defines the order of construction steps and is associated with **Builder**. And this **Director** class is called from a **Client** class.

**When To Use**:
- Use the builder pattern to get rid of the telescopic or giant constructor.
- Use the builder pattern when you want to create different representations of some product or object.
- Use the pattern to build complex objects like composite trees.

**Implementation**:
```java
public class House {
    private final int numberOfRoom;
    private final int numberOfWashroom;
    private final int numberOfWindow;
    private final int numberOfDoorPerRoom;
    private final int numberOfSouthFacingWindow;
    private final int numberOfKitchen;

    public House (int numberOfRoom, int numberOfWashroom, int numberOfWindow, int numberOfDoorPerRoom, int numberOfSouthFacingWindow, int numberOfKitchen) {
        this.numberOfRoom = numberOfRoom;
        this.numberOfWashroom = numberOfWashroom;
        this.numberOfWindow = numberOfWindow;
        this.numberOfDoorPerRoom = numberOfDoorPerRoom;
        this.numberOfSouthFacingWindow = numberOfSouthFacingWindow;
        this.numberOfKitchen = numberOfKitchen;
    }
}

public interface HouseBuilder {
    void setNumberOfRoom(int num);
    void setNumberOfWashroom(int num);
    void setNumberOfWindow(int num);
    void setNumberOfDoorPerRoom(int num);
    void setNumberOfSouthFacingWindow(int num);
    void setNumberOfKitchen(int num);
}

public class ConcreteHouseBuilder implements HouseBuilder {
    private int numberOfRoom;
    private int numberOfWashroom;
    private int numberOfWindow;
    private int numberOfDoorPerRoom;
    private int numberOfSouthFacingWindow;
    private int numberOfKitchen;

    @Override
    public void setNumberOfRoom(int num) {
        this.numberOfRoom = num;
    }

    @Override
    public void setNumberOfWashroom(int num) {
        this.numberOfWashroom = num;
    }

    @Override
    public void setNumberOfWindow(int num) {
        this.numberOfWindow = num;
    }

    @Override
    public void setNumberOfDoorPerRoom(int num) {
        this.numberOfDoorPerRoom = num;
    }

    @Override
    public void setNumberOfSouthFacingWindow(int num) {
        this.numberOfSouthFacingWindow = num;
    }

    @Override
    public void setNumberOfKitchen(int num) {
        this.numberOfKitchen = num;
    }

    public House getHouse() {
        return new House(numberOfRoom, numberOfWashroom, numberOfWindow, numberOfDoorPerRoom, numberOfSouthFacingWindow, numberOfKitchen);
    }
}

public class Director {

    public void constructHouse(HouseBuilder builder) {
        builder.setNumberOfRoom(2);
        builder.setNumberOfWashroom(4);
        builder.setNumberOfWindow(5);
        builder.setNumberOfDoorPerRoom(1);
        builder.setNumberOfSouthFacingWindow(2);
        builder.setNumberOfKitchen(1);
    }
}

public class Demo {

    public static void main(String[] args) {
        Director director = new Director();

        ConcreteHouseBuilder builder = new ConcreteHouseBuilder();
        director.constructHouse(builder);

        Car car = builder.getHouse();
    }
} 
```
Another Java implementation of builder design pattern can find [here](https://github.com/sir-rasel/Design-Pattern-Practice/tree/main/Creational%20Design%20Pattern/BuilderDesignPattern/Java/BuilderDesignPattern/src/main/java/org/example).

Builder pattern has another out of box and easy implementation. Like the following:
```java
public class Computer {
	
	private String HDD;
	private String RAM;
	private boolean isGraphicsCardEnabled;
	private boolean isBluetoothEnabled;
	

	public String getHDD() {
		return HDD;
	}

	public String getRAM() {
		return RAM;
	}

	public boolean isGraphicsCardEnabled() {
		return isGraphicsCardEnabled;
	}

	public boolean isBluetoothEnabled() {
		return isBluetoothEnabled;
	}
	
	private Computer(ComputerBuilder builder) {
		this.HDD=builder.HDD;
		this.RAM=builder.RAM;
		this.isGraphicsCardEnabled=builder.isGraphicsCardEnabled;
		this.isBluetoothEnabled=builder.isBluetoothEnabled;
	}
	
	//Builder Class
	public static class ComputerBuilder{

		private String HDD;
		private String RAM;
		private boolean isGraphicsCardEnabled;
		private boolean isBluetoothEnabled;
		
		public ComputerBuilder(String hdd, String ram){
			this.HDD=hdd;
			this.RAM=ram;
		}

		public ComputerBuilder setGraphicsCardEnabled(boolean isGraphicsCardEnabled) {
			this.isGraphicsCardEnabled = isGraphicsCardEnabled;
			return this;
		}

		public ComputerBuilder setBluetoothEnabled(boolean isBluetoothEnabled) {
			this.isBluetoothEnabled = isBluetoothEnabled;
			return this;
		}
		
		public Computer build(){
			return new Computer(this);
		}
	}
}

public class TestBuilderPattern {

	public static void main(String[] args) {
		Computer comp = new Computer.ComputerBuilder(
				"500 GB", "2 GB").setBluetoothEnabled(true)
				.setGraphicsCardEnabled(true).build();
	}

}
```

For small and single variation object, it can be feel as over engineering but for big and with lots of variation of a object builder pattern is a very handy tool.

---

## Achieved Design Principles:
- **Single Responsibility Principle (SRP)**: We can achieve SRP by these design patterns. Because different ConcreteBuilder classes can contain their own responsibilities.
- **Open/Closed Principle (OCP)**: We can achieve OCP by these design patterns. Because we can extend and create a new ConcreteBuilder class for adding new representations without modifying the existing ones.
- **Interface Segregation (IS)**: We can achieve IS by these design patterns. Because the Builder interface and different ConcreteBuilder classes can depend on different interfaces.