---
title: "Tale of Software Architect(ure): Part 13 (Clean Architecture)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-13T00:00:00Z"
tags: ["software-architect", "software-architecture", "software-design", "clean-architecture"]
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
    image: "img/blogs/95-software-architecture-clean.png"
    caption: "Clean Architecture"
    alt: "Clean Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 12:** [Tale of Software Architect(ure): Part 12 (Service Oriented Architecture)]({{< ref "blogs/94-software-architecture-soa.md" >}})
- **Part 14:** [Tale of Software Architect(ure): Part 14 (Modular Monolith Architecture Pattern)]({{< ref "blogs/96-software-architecture-modular-monolith.md" >}})
---

{{< figure
    src="/img/blogs/95-software-architecture-clean.png"
    caption="Clean Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the clean architecture pattern.

So let's get started...

---

## Story

In this world, Allah is the most powerful and only independent who doesn't need any help or something like that. Allah creates the whole world and all the creatures. Human is one of the best creature of Allah. He also creates a dependency chain that should be followed for maintaining the balance. If anyone want to break the chain or so called break the rules then a very unexpected and dangerous things happen. Which cost a very big damage in the system.

In the right hand part of the below picture, I try to draw a dependency flow of the universe where Allah (SWT) is one and only independent and all other parts are dependent of him directly or indirectly.

* * *

## Clean Architecture:
{{< figure
    src="/img/blogs/95-clean-architecture.jfif"
    caption="Clean Architecture (Photo Credit: Left hand: Uncle bob, Right hand : Myself)"
    align=center
>}}

Clean architecture is a software design philosophy that separates the elements of a design into ring levels, introduced by Robert C. Martin (Uncle Bob) in his book Clean Architecture: A Craftsman’s Guide to Software Structure and Design. More precisely, clean architecture, also known as onion architecture, is a software design architecture guideline that maintains a dependency rule: only point inwards. Means, like the above picture shows, all of the parts of the source code are dependent on Entity. Also, all the creatures of the world depend on Allah (SWT).

The main idea is to create a system that is flexible, maintainable, and independent of frameworks, databases, UI, or any external services. This is achieved by organizing code into layers, ensuring that each layer has a clear responsibility and that core business logic remains isolated from implementation details.

Layer of clean architecture in general:

1. **Core Layer**: 
The domain layer and application layer are combinedly called the core layer. Because these 2 layers are the heart of the clean architecture. All the other parts, like infrastructure, presentation, test, etc., depend on these 2 layers. That is why together they are called the core layer.

- Domain Layer:

The domain layer in the clean architecture contains the enterprise logic, like the entities and their specifications. This layer lies in the center of the architecture where we have application entities, which are the application model classes or database model classes. Using the code-first approach in the application development using different ORMs, these entities are used to create the tables in the database.

- Application Layer:

The application layer contains the business logic. All the business logic will be written in this layer. It is in this layer that service interfaces are kept, separate from their implementation, for loose coupling and separation of concerns.

2. **Infrastructure Layer**:

In the infrastructure layer, we have model objects. We will maintain all the database migrations and database context objects in this layer. In this layer, we have the repositories of all the domain model objects. Also, interface implementation is defined in the application layer.

3. **Presentation Layer**:

It can be API controllers or any UI. In the case of the API presentation layer, it presents us the object data from the database using the HTTP request in the form of a JSON object. But in the case of front-end applications, we present the data using the UI by consuming the APIs.

Key Concepts of Clean Architecture:

*   **Layered Structure (Onion-like or Concentric Circles)**: Clean Architecture is often visualized as a set of concentric circles, with each layer representing a different level of abstraction. Each layer can only depend on the layer directly inside it (higher-level layers depend on lower-level layers, not the reverse).
*   **Dependency Rule**: The dependency rule dictates that source code dependencies can only point inwards. The outer layers depend on the inner layers, but the inner layers should have no knowledge of the outer ones. This makes the core logic independent of external concerns (frameworks, databases, or UIs).
*   **Boundaries**: A key feature of Clean Architecture is the establishment of boundaries, using interfaces to separate the different layers. This ensures that each layer interacts with the adjacent layers in a controlled, predictable way.

## Context

In software development, it is common to build systems that are initially easy to manage but become hard to maintain as they grow. Typically, these systems have tightly coupled components like user interfaces, databases, and business logic, making it difficult to make changes without breaking things or introducing bugs.

Developers often struggle to keep their codebases flexible, testable, and maintainable over time. Frameworks evolve, databases change, and new user interfaces are required. These changes often result in complex refactoring efforts that lead to brittle code and high development costs.

## Problem

The main problem is tight coupling between the different layers of an application, especially between the business logic, frameworks, and external services. This creates several issues:

*   **Framework Dependency**: The business logic is tightly bound to the framework or database in use. Changing or upgrading a framework may break core application logic.
*   **Difficult to Test**: With logic mixed up between UI, database, and core operations, testing individual pieces of the application in isolation becomes difficult. You may need to spin up a full database or web server to test basic business logic.
*   **Complex Refactoring**: Even small changes in one part of the system can lead to ripple effects in other parts, making refactoring and extending the application difficult.
*   **Poor Maintainability**: As the codebase grows, the system becomes increasingly hard to understand and maintain, increasing the chance of introducing bugs when making updates or feature changes.

## Solution

Clean Architecture provides a structured approach to solving these problems by separating the application into layers, with clear boundaries and dependency rules:

1. **Separation of Concerns**: The architecture defines distinct layers (entities, use cases, interface adapters, frameworks/drivers), each responsible for a specific type of functionality. This makes the system more understandable and easier to maintain.

*   **Core Business Logic (Entities)**: Contains the high-level rules and is completely independent of external services or frameworks. This means you can change frameworks, databases, or UI without affecting this layer.
*   **Application Logic (Use Cases)**: Encapsulates application-specific logic and coordinates the interaction between entities. It is focused on solving specific business needs (e.g., placing an order) without knowing how the data is persisted or presented.
*   **Interface Adapters**: Translates data between the internal system and external components like UI, databases, or APIs. This ensures the core business logic is shielded from external changes.
*   **Frameworks/Drivers**: External services like the database, UI, or payment gateway reside here. The business logic doesn’t depend on these details, making the application more adaptable to change.

2. **Dependency Rule**: Clean Architecture dictates that dependencies flow inwards (towards core business logic). The innermost layers (entities, use cases) should know nothing about outer layers (frameworks, UI, or databases). Outer layers depend on the inner layers by adhering to the inversion of control principle (e.g., using interfaces to decouple dependencies).

3. **Testability and Flexibility**: By isolating business logic from external dependencies, Clean Architecture enables easier testing. Each layer can be tested in isolation without requiring real databases or external services. This increases confidence in refactoring and adding new features.

4. **Maintainability**: The architecture encourages writing clear, modular code that separates business logic from implementation details. This improves long-term maintainability, as developers can change external components (e.g., switching from SQL to NoSQL) without modifying the core system.

* * *

## Practical Example: E-Commerce Order System

Let’s apply Clean Architecture principles to an order processing system for an e-commerce platform.

**Entities (Core Business Logic)**:

*   Entities might include classes like Order, Customer, and Product.
*   The Order entity would have the logic for calculating the total price, adding or removing items, and checking inventory.
*   These classes are completely unaware of the database, UI, or how orders are presented to users. They just encapsulate the business rules.

```python
class Order:
    def __init__(self):
        self.items = []

    def add_item(self, product, quantity):
        # Business logic for adding an item
        self.items.append((product, quantity))

    def calculate_total(self):
        return sum([product.price * quantity for product, quantity in self.items])        
```

**Use Cases (Application Logic)**:

*   This layer would contain use cases like PlaceOrder or CalculateShipping.
*   The PlaceOrder use case uses the Order entity to ensure that an order is valid and can be processed.
*   It also handles business logic, such as checking if the customer has enough balance to place the order or if the products are in stock.

```python
class PlaceOrder:
    def __init__(self, order_repo, payment_service):
        self.order_repo = order_repo
        self.payment_service = payment_service

    def execute(self, order, customer):
        # Ensure the order is valid
        if order.calculate_total() > customer.balance:
            raise Exception("Insufficient balance")
        # Handle payment processing
        self.payment_service.process_payment(customer, order.calculate_total())
        # Store the order
        self.order_repo.save(order)        
```

**Interface Adapters (Data Transformation)**:

*   This layer adapts the data for use by the inner layers. For example, if you're using a database, you'd have a repository interface here to adapt database rows to domain objects.
*   These adapters translate the format of the data used by the business logic to the one expected by external systems like databases or UI.

```python
class OrderRepository:
    def __init__(self, db):
        self.db = db

    def save(self, order):
        # Convert order to database format and save
        self.db.insert("orders", {"items": order.items, "total": order.calculate_total()})        
```

**Frameworks and Drivers (External Services)**:

*   This layer contains frameworks, databases, or external services like payment gateways.
*   For example, a payment processing service or database connector would reside here.
*   If we change the database from MySQL to MongoDB, we only need to modify this layer, without affecting the business logic.

```python
class PaymentService:
    def process_payment(self, customer, amount):
        # External service handling the payment
        external_payment_gateway.charge(customer.account, amount)        
```

* * *

## Summary:

Clean Architecture is a software design philosophy created by Robert C. Martin (Uncle Bob) that aims to produce systems that are flexible, maintainable, and independent of frameworks, databases, or external services. The main goal is to separate concerns by organizing code into layers, ensuring that core business logic (entities) is isolated from implementation details like UI, databases, and frameworks. It promotes creating adaptable and resilient systems by isolating business logic from external dependencies and organizing the codebase into well-defined, decoupled layers.