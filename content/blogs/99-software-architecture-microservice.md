---
title: "Tale of Software Architect(ure): Part 17 (Microservice Architecture)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-17T00:00:00Z"
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
    image: "img/blogs/99-software-architecture-microservice.png"
    caption: "Micro-service Architecture"
    alt: "Micro-service Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 16:** [Tale of Software Architect(ure): Part 16 (Domain Driven Design)]({{< ref "blogs/98-software-architecture-ddd.md" >}})
- **Part 18:** [Tale of Software Architect(ure): Part 18 (Event Driven Architecture)]({{< ref "blogs/100-software-architecture-eda.md" >}})
---

{{< figure
    src="/img/blogs/99-software-architecture-microservice.png"
    caption="Micro-service Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the micro-service architecture pattern.

So let's get started...

---

## Story:

Imagine a small town bakery called "Sweet Slice", famous for its cakes, cookies, and custom pastries. Business is booming, and customers flood the bakery each day with different needs. Some come for cakes, others for fresh bread, and some for a quick coffee. At first, the bakery runs as one large unit, with every employee handling every task like taking orders, baking, handling payments, and packing. But as demand grows, this all-in-one approach causes problems:

*   Long lines develop because each employee tries to handle multiple tasks.
*   Errors happen frequently since it’s hard to manage so many orders at once.
*   If one employee is absent, everything slows down.

Seeing the chaos, the bakery’s owner, Komola, decides to break up the team into smaller, specialized roles. She hires dedicated staff for Order Taking, Baking, Packing, and Payment Handling.

With each person focused on their specific tasks, Sweet Slice runs smoothly. Customers get their orders faster, mistakes are reduced, and Komola can even hire extra hands in busy seasons for any role that’s overwhelmed like adding more bakers on holidays. Plus, if someone is sick, Komola can shift responsibilities or replace just that role without disrupting the whole operation.

* * *

## Microservice Architecture:
{{< figure
    src="/img/blogs/99-microservice-architecture.jfif"
    caption="Micro-service Architecture (Photo Credit: Middleware.io)"
    align=center
>}}

Microservice architecture is a software design approach where a large application is broken down into smaller, loosely coupled services, each responsible for a specific function. Each microservice can be developed, deployed, and maintained independently, often by different teams. This contrasts with a monolithic architecture, where all functions are tightly integrated into one large system.

Key Component / Concepts of Microservices:

1.  **Independent service**: Each microservice is a standalone unit with its own database, enabling teams to make changes without affecting other services.
2.  **API Gateway**: Acts as a central entry point, managing requests from clients and routing them to the appropriate services.
3.  **Scalability**: Microservices can scale individually based on demand, allowing better resource allocation.
4.  **Decentralized Database Per Service**: Each microservice manages its own data, which helps avoid a single point of failure and makes it easier to update and evolve each service independently.
5.  **Service Registry and Discovery**: Keeps track of service instances and allows services to find each other (often automated by tools like Consul or Eureka).
6.  **Inter-Service Communication**: Microservices communicate through lightweight protocols, typically HTTP/REST, gRPC, or message brokers like Kafka or RabbitMQ.
7.  **Load Balancer**: Distributes incoming requests across service instances, ensuring efficient resource usage and high availability.
8.  **Monitoring and Logging**: Provides real-time insights into service health, traffic, and error tracking. Tools like Prometheus and ELK Stack (Elasticsearch, Logstash, and Kibana) are commonly used.
9.  **Resilience**: Failures in one microservice do not bring down the whole application. For instance, if the payment service in an e-commerce platform is down, users can still browse products.
10.  **Service Orchestration and Management**: Manages deployment, scaling, and operation of microservices, often through container orchestration tools like Kubernetes.

## Practical Example: E-Commerce Platform

Imagine a large e-commerce application broken down into the following microservices:

1.  User Service: Manages user data, authentication, and profiles.
2.  Product Service: Handles product listings, details, inventory, and categorization.
3.  Cart Service: Manages shopping cart sessions and items within a cart.
4.  Order Service: Handles the creation and tracking of orders.
5.  Payment Service: Processes payments through third-party payment gateways.
6.  Notification Service: Sends emails or SMS notifications for order confirmations, status updates, and promotions.

Each service has its own responsibilities and can be scaled as needed. For instance:

*   If the Cart Service experiences high traffic, only this service can be scaled up without affecting the rest.
*   Updates can be deployed to the Payment Service independently, ensuring minimal downtime and isolating changes that only affect payment functionality.

* * *

## Context

A large application for example an e-commerce platform needs to support millions of users, each engaging with various features such as browsing products, adding items to a cart, placing orders, making payments, and receiving notifications. The system must be highly available, scalable, and resilient to failures. Additionally, it must support rapid development and deployment, allowing for regular feature updates without impacting the entire system.

## Problem

In a traditional monolithic architecture, all components like (user management, product catalog, order processing, payments, and notifications) would be tightly coupled into a single application. This setup presents several issues:

*   **Scalability Issues**: Scaling the entire monolithic application is costly and inefficient, as traffic may spike only for specific features (e.g., payments during sales).
*   **Slow Deployment Cycles**: Any change or new feature requires redeploying the entire application, slowing down development and increasing the risk of downtime.
*   **Fault Tolerance Challenges**: A failure in one part of the application (e.g., a bug in the order processing) could bring down the entire system, leading to a poor user experience.
*   **Development Bottlenecks**: Teams have to work on shared codebases, making collaboration harder, especially as the application grows.

## Solution

The Microservice Architecture approach addresses these issues by breaking the large application into distinct, loosely coupled services, each responsible for a specific function such as:

1.  User Service: Manages authentication and user data.
2.  Product Service: Handles product listings, inventory, and details.
3.  Cart Service: Manages shopping cart operations and persistence.
4.  Order Service: Manages order creation, processing, and tracking.
5.  Payment Service: Manages payment transactions with external providers.
6.  Notification Service: Sends email/SMS notifications for updates and promotions.

How This Solves the Problem:

*   **Scalability**: Each service can be scaled independently based on demand. For example, if there’s a high volume of orders during a sale, only the Order Service and Payment Service need to scale, saving resources.
*   **Faster Development & Deployment**: Services can be updated and deployed independently, so changes to the Payment Service do not affect the User Service. This allows for rapid, isolated feature releases with minimal risk of downtime.
*   **Improved Fault Tolerance**: Failures are isolated to individual services. For example, if the Notification Service fails, users can still place orders and complete payments.
*   **Agility in Development**: Smaller, dedicated teams can work on specific services without stepping on each other’s toes, increasing productivity and reducing bottlenecks.

* * *

## Sample Pseudocode:

Here’s a pseudocode example demonstrating how an Order Service in a microservice-based e-commerce application might work, coordinating with other microservices. This example uses pseudocode to outline the order workflow, including calls to the User Service, Product Service, Payment Service, and Notification Service.

```python
# Order Service
class OrderService:
    def place_order(user_id, cart_items):
        # Step 1: Verify User
        user_data = UserService.get_user(user_id)
        if not user_data:
            return "User not found"
        
        # Step 2: Validate Cart Items
        available_products = []
        for item in cart_items:
            product = ProductService.check_availability(item.product_id, item.quantity)
            if product is not available:
                return f"Product {item.product_id} is out of stock"
            available_products.append(product)
        
        # Step 3: Reserve Products
        for product in available_products:
            ProductService.reserve_product(product.id, product.quantity)
        
        # Step 4: Process Payment
        payment_status = PaymentService.process_payment(user_id, calculate_total(cart_items))
        if payment_status != "Success":
            for product in available_products:
                ProductService.release_reservation(product.id)
            return "Payment failed"
        
        # Step 5: Create Order
        order = create_order(user_id, cart_items)
        
        # Step 6: Notify User
        NotificationService.send_notification(
            user_id, 
            f"Order {order.id} placed successfully. Total amount: {calculate_total(cart_items)}"
        )
        
        return f"Order {order.id} has been successfully placed"

    def calculate_total(cart_items):
        total = 0
        for item in cart_items:
            total += item.price * item.quantity
        return total


# User Service (Microservice for managing users)
class UserService:
    def get_user(user_id):
        # Retrieve user data from the User Service database
        return user_database.get(user_id)


# Product Service (Microservice for managing products and inventory)
class ProductService:
    def check_availability(product_id, quantity):
        # Check if the product is available in the required quantity
        product = product_database.get(product_id)
        return product if product.stock >= quantity else None
    
    def reserve_product(product_id, quantity):
        # Deduct quantity from stock for reservation
        product = product_database.get(product_id)
        product.stock -= quantity

    def release_reservation(product_id):
        # Re-add quantity back to stock if payment fails
        product = product_database.get(product_id)
        product.stock += quantity


# Payment Service (Microservice for handling payments)
class PaymentService:
    def process_payment(user_id, amount):
        # Mock payment processing logic
        payment_success = external_payment_gateway.charge(user_id, amount)
        return "Success" if payment_success else "Failure"


# Notification Service (Microservice for sending notifications)
class NotificationService:
    def send_notification(user_id, message):
        # Send email or SMS to the user
        notification_system.send(user_id, message)


# Example Usage
user_id = "user123"
cart_items = [
    {"product_id": "prod001", "quantity": 2, "price": 20.0},
    {"product_id": "prod002", "quantity": 1, "price": 50.0}
]

# Place an order
order_service = OrderService()
order_status = order_service.place_order(user_id, cart_items)
print(order_status)  # Output: Order XYZ has been successfully placed        
```

* * *

## Summary:

Microservice architecture is a design approach that breaks down a large application into smaller, independent services, each responsible for a specific function. These "microservices" operate independently but work together to fulfill application needs. Each service can be developed, deployed, and scaled separately, often with its own database and team.

Key Benefits:

*   **Scalability**: Services can be scaled individually based on demand.
*   **Resilience**: Failures in one service don't bring down the whole system.
*   **Faster Development and Deployment**: Updates and changes can be made to individual services without affecting the others.
*   **Improved Agility**: Allows specialized teams to work independently, speeding up development.

In essence, microservices increase flexibility and reliability by decentralizing responsibilities within an application.