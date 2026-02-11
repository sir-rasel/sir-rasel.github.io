---
title: "Tale of Software Architect(ure): Part 18 (Event Driven Architecture)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-18T00:00:00Z"
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
    image: "img/blogs/100-software-architecture-eda.png"
    caption: "Event Driven Architecture"
    alt: "Event Driven Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 17:** [Tale of Software Architect(ure): Part 17 (Microservice Architecture)]({{< ref "blogs/99-software-architecture-microservice.md" >}})
---

{{< figure
    src="/img/blogs/100-software-architecture-eda.png"
    caption="Event Driven Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the event driven architecture pattern.

So let's get started...

---

## Story:

Once upon a time there was a popular marketplace called "Cloud Bazaar." Vendors in Cloud Bazaar worked around the clock to fulfill orders and delight their customers. However, as the city grew, so did the number of orders, making it difficult for vendors to keep up. The once-efficient market was bogged down by delays and dependencies between services.

To solve this problem, the president of Cloud Bazaar introduced a new communication system called "Order & Chill". In this system, every vendor and service would operate independently but would stay connected through a network of messengers called "Brokers."

Here’s how it worked: When a customer ordered something, the "Order Desk" would place an "Order Placed" message on the Broker’s board. This board was a special place where all services could see the new events and pick up tasks that concerned them.

With this new system, each service could act as soon as they saw the relevant message on the board without waiting for each other. No one was held up by dependencies, and any new team, like a Loyalty Points service, could simply start listening for events that mattered to them without affecting anyone else.

* * *

### Event Driven Architecture:
{{< figure
    src="/img/blogs/100-eda-architecture.png"
    caption="Event Driven Architecture (Photo Credit: Hazelcast)"
    align=center
>}}

Event-driven architecture (EDA) is a software architecture pattern in which system components communicate through events instead of direct requests. It’s ideal for systems that need to respond to a series of unpredictable events in real-time or systems that not need immediate response, allowing for greater flexibility and scalability.

Key Components of Event-Driven Architecture:

1.  **Event Producers**: Components that generate events when something of interest happens. For instance, an e-commerce website might generate an event when a user places an order.
2.  **Event Consumers**: Components that listen for specific events and react to them. Consumers are often unaware of who produced the event, promoting loose coupling.
3.  **Event Broker**: A middle layer that routes events from producers to consumers. Brokers, such as Kafka or RabbitMQ, store events and handle the logic of which events go to which consumers.
4.  **Event**: A discrete record of something that happened, carrying necessary data to inform consumers about the context.

## Example Scenario: E-commerce Order Processing

Let's consider an online retail platform to illustrate event-driven architecture:

**Order Placed (Event Producer)**

*   When a user places an order, the platform generates an Order Placed event. This event includes details like order ID, items ordered, user information, and payment details.

**Event Broker (e.g., Kafka or RabbitMQ)**

*   The Order Placed event is sent to an event broker. The broker temporarily stores the event and manages the distribution to multiple interested consumers.

**Event Consumers**

*   Inventory Service: Subscribed to the Order Placed event, it reduces the stock for each ordered item and triggers an Inventory Updated event if needed.
*   Shipping Service: Picks up the Order Placed event to start packaging and shipping preparation.
*   Billing Service: Receives the Order Placed event to initiate the payment process and validate funds. Once complete, it generates an Order Billed event.

**Further Events and Reactions**

*   Once the Order Billed event is published, additional consumers can react to it: Email Notification Service: Sends a confirmation email to the customer. Customer Loyalty Service: Adds loyalty points to the customer’s account based on the order value.

* * *

## Context

Modern software systems often require scalability, real-time responsiveness, and adaptability to handle diverse, unpredictable events. These systems, such as e-commerce platforms, financial trading systems, and IoT applications, need to process and respond to user actions or external triggers promptly without being bound to a strict sequence. Traditional architectures, like monolithic or request-driven designs, can struggle with such real-time demands and can become complex and rigid as they grow, especially when new features are added.

## Problem

1.  **Tight Coupling and Scalability Limitations**: In traditional architectures, components often directly communicate with one another. This creates dependencies, making it difficult to add, modify, or scale individual services without affecting others.
2.  **Inefficiency in Real-Time Processing**: Traditional systems that process requests synchronously or in sequence can introduce bottlenecks and delays, as each component may need to wait for the previous one to finish. This is inefficient in systems where many components need to act on the same event concurrently.
3.  **Limited Flexibility for Expanding Functionality**: When new features or services are added, existing systems often require major adjustments, which can lead to lengthy development cycles, higher costs, and increased chances of introducing bugs.

## Solution

Event-Driven Architecture (EDA) introduces a model where:

*   **Components Communicate Through Events**: Instead of direct requests, components produce and consume events. An event represents a significant change or action, like a user placing an order.
*   **Loose Coupling and Scalability**: Components are loosely coupled via an event broker (e.g., Kafka, RabbitMQ). The broker routes events to consumers, ensuring that producers (e.g., order processing) don’t need to know which services (e.g., billing, shipping) will handle their events.
*   **Real-Time and Asynchronous Processing**: Multiple services can react to the same event simultaneously, enabling real-time responses and increased efficiency. For instance, an Order Placed event can trigger inventory checks, payment processing, and shipping preparations concurrently.

* * *

## Sample Pseudocode:

**Step 1: Define Event Data Structure**

First, define a basic structure for an event, which will contain event type and event data.

```python
# Event structure
class Event:
    def __init__(self, type, data):
        self.type = type
        self.data = data        
```

**Step 2: Event Broker**

The broker will manage events and route them to the appropriate consumers.

```python
# Event Broker for managing events
class EventBroker:
    def __init__(self):
        self.subscribers = {}  # Dictionary to store event type and corresponding subscribers

    def subscribe(self, event_type, handler):
        if event_type not in self.subscribers:
            self.subscribers[event_type] = []
        self.subscribers[event_type].append(handler)

    def publish(self, event):
        if event.type in self.subscribers:
            for handler in self.subscribers[event.type]:
                handler(event)        
```

**Step 3: Define Event Producers**

The OrderService acts as the producer when an order is placed. It publishes an Order Placed event.

```python
# Order Service that produces events
class OrderService:
    def __init__(self, broker):
        self.broker = broker

    def place_order(self, order_data):
        print("Order placed:", order_data)
        event = Event("OrderPlaced", order_data)
        self.broker.publish(event)        
```

**Step 4: Define Event Consumers**

Each service subscribes to specific events and defines how to handle them.

```python
# Inventory Service - subscribes to OrderPlaced event
class InventoryService:
    def __init__(self, broker):
        broker.subscribe("OrderPlaced", self.update_inventory)

    def update_inventory(self, event):
        print("Inventory updated for order:", event.data)

# Billing Service - subscribes to OrderPlaced event
class BillingService:
    def __init__(self, broker):
        broker.subscribe("OrderPlaced", self.process_payment)

    def process_payment(self, event):
        print("Payment processed for order:", event.data)
        # Publish another event after billing is complete
        order_billed_event = Event("OrderBilled", event.data)
        broker.publish(order_billed_event)

# Shipping Service - subscribes to OrderPlaced and OrderBilled events
class ShippingService:
    def __init__(self, broker):
        broker.subscribe("OrderPlaced", self.prepare_shipping)
        broker.subscribe("OrderBilled", self.ship_order)

    def prepare_shipping(self, event):
        print("Preparing shipment for order:", event.data)

    def ship_order(self, event):
        print("Shipping order:", event.data)

# Notification Service - subscribes to OrderBilled event
class NotificationService:
    def __init__(self, broker):
        broker.subscribe("OrderBilled", self.send_confirmation)

    def send_confirmation(self, event):
        print("Confirmation email sent for order:", event.data)        
```

**Step 5: Putting It All Together**

Initialize the broker, services, and simulate an order being placed.

```python
# Initialize the event broker
broker = EventBroker()

# Initialize services and subscribe them to events
inventory_service = InventoryService(broker)
billing_service = BillingService(broker)
shipping_service = ShippingService(broker)
notification_service = NotificationService(broker)

# Simulate placing an order
order_service = OrderService(broker)
order_data = {"order_id": 123, "items": ["item1", "item2"], "total": 100.0}
order_service.place_order(order_data)        
```

* * *

## Summary:

Event-driven architecture (EDA) is a software design pattern where components communicate through events rather than direct calls. In this architecture, event producers generate events when something significant happens (e.g., a user places an order), and event consumers listen for these events to perform relevant actions (e.g., processing payment, updating inventory). Events are routed through an event broker, which stores and delivers them to all interested consumers.

EDA is ideal for building scalable, flexible systems, as each component can operate independently and respond in real time, allowing for efficient handling of complex workflows without creating bottlenecks. New consumers can easily be added without altering existing ones, supporting system growth and flexibility.