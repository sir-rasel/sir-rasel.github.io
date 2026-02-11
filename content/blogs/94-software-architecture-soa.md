---
title: "Tale of Software Architect(ure): Part 12 (Service Oriented Architecture)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-12T00:00:00Z"
tags: ["software-architect", "software-architecture", "software-design"]
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
    image: "img/blogs/94-software-architecture-soa.png"
    caption: "Service Oriented Architecture"
    alt: "Service Oriented Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 11:** [Tale of Software Architect(ure): Part 11 (Microkernel Architecture)]({{< ref "blogs/93-software-architecture-micro-kernel.md" >}})
- **Part 13:** [Tale of Software Architect(ure): Part 13 (Clean Architecture)]({{< ref "blogs/95-software-architecture-clean.md" >}})
---

{{< figure
    src="/img/blogs/94-software-architecture-soa.png"
    caption="Service Oriented Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the service oriented software architecture pattern.

So let's get started...

---

## Story:

In a kingdom called **GanjamLand**, the king struggled to manage the ever-growing needs of his people due to a massive, complicated infrastructure or large arrangement where every change disrupted the entire system. A wise architect proposed a new approach: instead of expanding the complicated arrangement, they built a village of small, independent houses, each responsible for one task—such as handling payments, managing inventory, or sending notifications. These houses worked together but could grow or change independently without affecting others. This new system, known as **Service-Oriented Architecture (SOA)**, made the kingdom more efficient, adaptable, and easier to maintain.

* * *

## Service Oriented Architecture:
{{< figure
    src="/img/blogs/94-soa-architecture.png"
    caption="Service Oriented Architecture (Photo Credit: umairsaeed)"
    align=center
>}}

Service-Oriented Architecture (SOA) is a architecture pattern used in software development where services are provided to other components by application components through a network, typically via a communication protocol such as REST or gRpc. In SOA, different services work together to form a distributed application. Each service is a self-contained unit that performs a specific function and can be reused by different applications or systems.

**Components of SOA**

There are typically four main components in SOA:

1.  **Service**: This is the foundation of SOA. Services can be private and available only to authorized users or Open Source and publicly available. Each service contains a service implementation, which is the code responsible for performing the service; a service contract, which describes the parameters of a service and its cost and quality; and a service interface, which is the layer of a service that defines how to communicate with it and handles communication with other services and systems.
2.  **Service provider**: This component creates or provides the service. Most organizations either create their own service or use third-party services.
3.  **Service consumer**: The service consumer is the individual, system, application or other service that makes service requests to the service provider. The service contract describes the rules for interaction between a service provider and service requester.
4.  **Service registry**: Also known as a service repository, a service registry is a directory of available services. It is tasked with storing service descriptions and other relevant information about how to use a service provider's services.

## Context

Modern businesses and enterprises often rely on complex systems that involve numerous functionalities. Whether it's an e-commerce platform, a banking system, or a healthcare network, companies need systems that handle multiple tasks, such as processing transactions, managing customer data, and integrating third-party services.

Traditionally, these systems were developed as **monolithic** applications where all features and functionalities were tightly integrated into a single codebase. As businesses grow, these monolithic systems face several challenges:

*   **Scalability**: Scaling a monolithic application often means scaling the entire system, even if only a small part of it requires more resources.
*   **Maintenance**: Making changes or updates in one part of the system can have unintended consequences elsewhere, making the system difficult to maintain.
*   **Integration**: With an ever-increasing need to integrate external services or platforms (such as payment gateways, third-party APIs, or legacy systems), monolithic architectures struggle with flexibility and adaptability.

## Problem

Organizations need to:

*   **Rapidly adapt to new business requirements** without rewriting or overhauling entire systems.
*   **Scale specific parts of their system** independently based on demand (e.g. scaling user authentication services during peak login times without affecting other components).
*   **Reuse functionality across different applications** (e.g. using the same payment system for both a web app and a mobile app).
*   **Integrate diverse systems** that are built with different technologies (e.g. integrating a legacy inventory system with a modern e-commerce platform).
*   **Improve fault tolerance by isolating failures** so that a bug in one part of the system doesn’t bring down the entire application.

The challenge is to create a system that is modular, scalable, flexible, and maintainable, while also ensuring that all parts of the system can communicate seamlessly across different platforms.

## Solution

SOA addresses these problems by dividing the system into independent, loosely coupled services that communicate over a network. Each service is a self-contained unit that performs a specific business function and can be reused or scaled independently.

Key characteristics of the solution:

1.  **Decoupling and Modularity**: Services are designed to perform specific, discrete tasks (e.g. user authentication, inventory management, or payment processing). Since these services are independent, changes to one service do not affect others. This allows the system to evolve over time without causing ripple effects.
2.  **Scalability**: Each service can be scaled independently based on demand. For example, if the user login service is under heavy load, it can be scaled without needing to add resources to the payment service or product service.
3.  **Reusability**: Services are designed to be reusable across multiple applications. For instance, the same payment processing service could be used by both an e-commerce platform and a mobile app.
4.  **Interoperability and Integration**: SOA allows different services, possibly developed with different technologies, to communicate using standard protocols (e.g., HTTP, SOAP, REST, etc.). This allows easy integration of legacy systems, third-party services, and new applications into the same ecosystem.
5.  **Fault Tolerance**: Since services are independent, a failure in one service (e.g., payment) does not bring down the entire system. Other services, like product browsing or user authentication, can continue functioning, improving the system's resilience.
6.  **Orchestration**: More complex business processes (e.g., placing an order) can be created by orchestrating multiple services together. This allows for flexibility and agility in how business operations are managed, especially when business needs evolve over time.

## Example Solution:

**Context**: A growing e-commerce platform needs to handle a variety of functions like browsing products, processing payments, managing inventory, and shipping orders.

**Problem**: The current monolithic system struggles to keep up with demand. When traffic increases (e.g. during sales), the payment system overloads, causing the entire platform to slow down. Furthermore, updating one part of the system often introduces bugs in other areas, leading to frequent downtime.

**Solution**: Implement SOA by breaking down the system into independent services:
*   Product Service: Manages product listings, categories, and availability.
*   Payment Service: Handles secure payment processing and supports multiple payment providers.
*   Inventory Service: Tracks stock levels and updates quantities when orders are placed.
*   Notification Service: Sends order confirmations and delivery updates.
*   Shipping Service: Calculates shipping costs and tracks delivery progress.

Each of these services can now be scaled independently, making the system more robust and flexible. The platform can also integrate third-party shipping services or payment gateways with ease, thanks to SOA’s emphasis on interoperability.

* * *

## Pseudocode:

```python
# This is the Order Service that orchestrates the process of placing an order.
class OrderService:
    function placeOrder(orderDetails):
        # 1. Check product availability by calling Product Service
        productAvailable = ProductService.checkAvailability(orderDetails.productId)
    
        if not productAvailable:
            return "Product is out of stock"
    
        # 2. Process payment by calling Payment Service
        paymentSuccessful = PaymentService.processPayment(orderDetails.paymentDetails)
    
        if not paymentSuccessful:
            return "Payment failed"
    
        # 3. Reduce the stock by calling Inventory Service
        inventoryUpdated = InventoryService.reduceStock(orderDetails.productId, orderDetails.quantity)
    
        if not inventoryUpdated:
            return "Failed to update inventory"
    
        # 4. Send confirmation email by calling Notification Service
        NotificationService.sendEmail(orderDetails.customerEmail, "Order Confirmed", "Your order has been placed successfully.")
    
        return "Order placed successfully"

# Product Service: Checks if the product is in stock
class ProductService:
    function checkAvailability(productId):
        # Query the product database to see if stock is available
        stock = ProductDatabase.getStock(productId)
        if stock > 0:
            return true
        else:
            return false

# Payment Service: Processes the payment
class PaymentService:
    function processPayment(paymentDetails):
        # Interact with payment gateway (e.g., Stripe, PayPal)
        paymentResponse = PaymentGateway.process(paymentDetails)
        if paymentResponse.success:
            return true
        else:
            return false

# Inventory Service: Reduces stock once the order is placed
class InventoryService:
    function reduceStock(productId, quantity):
        stock = ProductDatabase.getStock(productId)
        if stock >= quantity:
            ProductDatabase.updateStock(productId, stock - quantity)
            return true
        else:
            return false

# Notification Service: Sends confirmation email to customer
class NotificationService:
    function sendEmail(toEmail, subject, body):
        # Send email using an email service provider
        EmailProvider.send(toEmail, subject, body)        
```

* * *

## Summary:

Service-Oriented Architecture (SOA) is an architectural style that enables the development of scalable, reusable, and loosely coupled services. It enhances system flexibility, maintainability, and interoperability, making it suitable for complex and large-scale enterprise applications. Despite the challenges of managing security, complexity, and governance, SOA continues to be a critical architecture for enterprises looking to build systems that can adapt to changing business needs.