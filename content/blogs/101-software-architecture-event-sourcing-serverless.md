---
title: "Tale of Software Architect(ure): Part 19 (Event Sourcing and Serverless Architecture Pattern)
"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-19T00:00:00Z"
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
    image: "img/blogs/101-software-architecture-serverless.png"
    caption: "Event Sourcing and Serverless Architecture"
    alt: "Event Sourcing and Serverless Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 18:** [Tale of Software Architect(ure): Part 18 (Event Driven Architecture)]({{< ref "blogs/100-software-architecture-eda.md" >}})
---

{{< figure
    src="/img/blogs/101-software-architecture-serverless.png"
    caption="Event Sourcing Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the event sourcing and serverless architecture pattern.

So let's get started...

---

## Event Sourcing Architecture Pattern:
{{< figure
    src="/img/blogs/101-event-sourcing-architecture.png"
    caption="Event Sourcing and Serverless Architecture (Photo Credit: Medium)"
    align=center
>}}

Event Sourcing is an architectural pattern in which the state of a system is derived by recording and storing a sequence of events, rather than directly saving the current state. These events represent changes in the system over time, and they are stored as an append-only log. The key idea is that every state change (or event) is stored as an immutable record, allowing the system to reconstruct the entire state by replaying these events from the start.

Key Concepts:

1.  **Events**: Represent a fact that has happened, such as "OrderPlaced", "OrderShipped" etc. Events are immutable, meaning they cannot be modified once they are created.
2.  **Event Store**: A database or storage mechanism specifically for storing events. It acts as the source of truth for all state changes in the system.
3.  **Event Stream**: A sequence of events tied to a particular entity or aggregate (such as a specific order or user).
4.  **Command Handling**: Commands (requests to change state, like "PlaceOrder") trigger events.
5.  **Projections**: Read-only views of data, created by processing event streams to reflect the current state. Projections help create query-optimized views of the data without needing to traverse the entire event log each time.

Benefits of Event Sourcing:

1.  **Auditability**: Every change is recorded, making it easy to trace and audit past states.
2.  **Data Recovery**: Since all events are stored, it's possible to reconstruct the entire state of the system from scratch if necessary.
3.  **Temporal Queries**: You can query what the state of the system was at any point in time.
4.  **Scalability**: Events can be handled asynchronously and processed in parallel for different aggregates.

## Practical Example

Let’s take the example of an e-commerce order management system. This system might use Event Sourcing to handle orders from placement through to delivery.

**Step 1: Commands Trigger Events**

Suppose a customer places an order. The following steps take place:

1.  Command: The system receives a PlaceOrder command with details such as product ID, quantity, and customer information.
2.  Event: The system then creates an OrderPlaced event with the order details and stores it in the event store.

**Step 2: Events Build System State**

The system processes the event stream to build the order’s current state:

1.  When OrderPlaced is recorded, the order state might be set to "Pending".
2.  When a warehouse ships the order, the system receives a ShipOrder command, triggering an OrderShipped event. The event is appended to the event log.
3.  If the customer receives the order, a DeliverOrder command triggers an OrderDelivered event, marking the order as "Completed".

**Step 3: Projecting Events into Read Models**

To enable faster access for queries:

1.  The system might project all OrderPlaced, OrderShipped, and OrderDelivered events into an "Order Summary" table in a read-optimized format, e.g., with fields like OrderID, Status, and DeliveryDate.
2.  This projection allows quick lookups of the current state of any order without replaying all events in real-time.

## Context

In many applications, particularly in systems with complex domains such as financial systems, e-commerce, and supply chain management, data consistency and traceability are crucial. Traditional CRUD (Create, Read, Update, Delete) approaches often overwrite data to represent the current state. This can make it difficult to:

*   Track historical changes
*   Revert to previous states
*   Audit past actions for regulatory or business insights

As businesses require a complete history of every change made to their data and the ability to reconstruct previous states, a more flexible approach to state management becomes necessary.

## Problem

In a traditional data management setup, applications typically store only the current state, discarding any historical data or transitions. This leads to several challenges:

1.  **Lack of History**: It’s hard to see what led to the current state, limiting insights and accountability.
2.  **Complexity in Restoring Previous States**: If errors occur or data needs to be analyzed as it was at a specific point in time, it can be very difficult (or impossible) to revert without a historical record.
3.  **Limited Auditability**: Many industries require the ability to audit changes to data, which becomes challenging when only the final state is saved.
4.  **Difficulty in Reproducing Issues**: Without knowing the sequence of changes, identifying the root cause of issues or reproducing bugs is difficult.
5.  **High Coupling Between Reads and Writes**: This makes it hard to optimize for scalable, real-time data views or queries.

## Solution

Event Sourcing addresses these problems by storing each state change as a distinct event in an append-only log. Rather than representing the current state directly in a database, the application saves a sequence of events that have occurred. This event log becomes the single source of truth for reconstructing state.

*   **Log of Events**: Every change is stored as an event, such as "OrderPlaced", "OrderShipped" or "PaymentProcessed" providing a full history of changes.
*   **Immutable Events**: Once recorded, events are immutable, ensuring data integrity and making it possible to reconstruct the state exactly as it was at any given time.
*   **Event Replay**: The current state of an entity can be derived by replaying its event history from the beginning.
*   **Projections**: To support efficient querying, the application can create projections, or materialized views, that summarize the current state without re-computing it every time.
*   **Flexibility for Analytics**: Since every event is stored, the application can reprocess and analyze data in new ways, providing insights such as the frequency of certain events or changes over time.

## Sample Pseudocode

Here’s a simplified code snippet in Python to demonstrate Event Sourcing for an order lifecycle.

```python
class OrderEvent:
    def __init__(self, order_id, event_type, data):
        self.order_id = order_id
        self.event_type = event_type
        self.data = data

class EventStore:
    def __init__(self):
        self.events = []
    
    def add_event(self, event):
        self.events.append(event)
    
    def get_events(self, order_id):
        return [e for e in self.events if e.order_id == order_id]

# Adding events
event_store = EventStore()
event_store.add_event(OrderEvent("1001", "OrderPlaced", {"customer": "John", "product": "Laptop"}))
event_store.add_event(OrderEvent("1001", "OrderShipped", {"warehouse": "WH1"}))
event_store.add_event(OrderEvent("1001", "OrderDelivered", {"delivery_service": "DHL"}))

# Replaying events to build order state
def get_order_status(order_id):
    events = event_store.get_events(order_id)
    status = "Unknown"
    for event in events:
        if event.event_type == "OrderPlaced":
            status = "Pending"
        elif event.event_type == "OrderShipped":
            status = "Shipped"
        elif event.event_type == "OrderDelivered":
            status = "Completed"
    return status

print(get_order_status("1001"))  # Output: Completed        
```

* * *

## Serverless Architecture Pattern:
{{< figure
    src="/img/blogs/101-serverless-architecture.png"
    caption="Serverless Architecture (Photo Credit: Markovate)"
    align=center
>}}

Serverless architecture is a cloud computing model where developers can build and deploy applications without managing the underlying infrastructure. In this pattern, the cloud provider handles server management, scaling, and maintenance. Developers focus on writing code, which runs in short-lived, event-driven functions triggered by specific actions. This makes serverless ideal for applications with unpredictable workloads and for functions that need to scale quickly.

Key Concepts:

1.  **Function as a Service (FaaS)**: In a serverless model, code is broken down into small, discrete functions, typically triggered by events (e.g., HTTP requests, database updates). These functions only run when triggered, which reduces idle time and costs.
2.  **Event-Driven Architecture**: Serverless applications respond to events, like user clicks or data uploads, triggering functions that handle specific tasks. These events can be generated by users, APIs, or system actions (e.g., file uploads).
3.  **Scalability**: Serverless platforms automatically scale the number of function instances in response to demand, ensuring that workloads are managed seamlessly without manual intervention.
4.  **Cost-Efficiency**: Serverless follows a pay-per-use model. Since functions only run in response to events, you only pay for the actual compute time, which can be more cost-effective than maintaining dedicated servers.
5.  **Statelessness**: Serverless functions are generally stateless, which means each function call is independent. For maintaining application state, serverless applications rely on external databases or storage solutions.

Benefits of Serverless in this Example:

Serverless architecture is particularly well-suited for applications requiring high elasticity, rapid scaling, and minimal maintenance. However, it's best for stateless, event-driven use cases and may be less ideal for long-running processes or applications needing persistent connections.

*   **Automatic Scaling**: The Lambda function scales automatically if multiple users upload images simultaneously, handling thousands of requests without requiring manual scaling.
*   **Reduced Costs**: Costs remain low, as charges apply only for the execution time of each function.
*   **Simplified Management**: Developers don’t need to manage a full backend system for image processing. They focus on the function's code, while AWS manages the scaling, execution, and monitoring.

## Context

In today’s fast-paced digital landscape, businesses are increasingly relying on cloud computing to deliver applications and services efficiently. Traditional server-based architectures require significant upfront investment in hardware, ongoing maintenance, and scaling challenges. As applications grow, managing infrastructure becomes cumbersome, and scaling to meet fluctuating demand can lead to either over-provisioning (wasting resources) or under-provisioning (leading to performance issues).

Developers need a way to deploy applications quickly, without the overhead of managing servers, while ensuring high availability and performance. This need for efficiency, agility, and cost-effectiveness has led to the adoption of serverless architecture.

## Problem

1.  **Infrastructure Management**: Developers spend a lot of time managing servers, patches, and scaling, which detracts from focusing on code and feature development.
2.  **Cost Inefficiency**: Organizations often pay for idle server capacity during low traffic periods, leading to higher operational costs without proportional benefits.
3.  **Scalability Challenges**: Sudden spikes in user demand can overwhelm traditional server infrastructures, resulting in downtime or degraded performance, negatively impacting user experience.
4.  **Development Bottlenecks**: Longer deployment cycles due to server management and configuration can slow down the release of new features or updates.

## Solution

Adopting Serverless Architecture: Serverless architecture addresses these challenges by allowing developers to build and deploy applications as a collection of stateless, event-driven functions, managed entirely by a cloud provider.

1.  **Focus on Code**: Developers can concentrate on writing application logic without worrying about provisioning or managing servers. This accelerates the development lifecycle and encourages innovation.
2.  **Pay-as-You-Go Pricing Model**: Organizations only pay for the actual compute time consumed by their functions, eliminating costs associated with idle server capacity and enabling better cost management.
3.  **Automatic Scalability**: Serverless platforms automatically scale functions up or down based on demand, ensuring applications can handle traffic spikes effortlessly without manual intervention.
4.  **Event-Driven Processing**: Functions can be triggered by various events (HTTP requests, database changes, etc.), enabling seamless integration with other services and creating responsive applications.
5.  **Simplified Maintenance**: The cloud provider handles server maintenance, updates, and scaling, freeing developers from routine operational tasks and allowing them to focus on enhancing application features.

## Practical Example

Consider an e-commerce platform that allows users to upload product images. By implementing serverless architecture:

*   **Context**: The platform needs to process images quickly and efficiently to maintain user engagement.
*   **Problem**: Traditional server setups can struggle with traffic spikes during sales events, leading to slow uploads and a poor user experience.
*   **Solution**: Using a serverless function (e.g., AWS Lambda) to handle image uploads allows the platform to process images on demand. Each upload triggers the function to resize and optimize images automatically, scaling seamlessly with the number of uploads. This eliminates infrastructure management overhead and provides cost savings, as the platform only pays for the processing time needed for each image.

## Sample Pseudocode

```js
// Define a function to handle image uploads
function handleImageUpload(event):
    // Extract the image URL from the event
    imageUrl = event.imageUrl

    // Call the function to process the image
    processedImageUrl = processImage(imageUrl)

    // Notify the user that the image has been processed
    notifyUser(event.userId, processedImageUrl)

// Define a function to process the image
function processImage(imageUrl):
    // Load the image from the given URL
    image = loadImage(imageUrl)

    // Apply filters or transformations to the image
    filteredImage = applyFilters(image)

    // Resize the image to a specified size
    resizedImage = resizeImage(filteredImage, width=800, height=600)

    // Save the processed image to storage (e.g., AWS S3)
    processedImageUrl = saveToStorage(resizedImage)

    // Return the URL of the processed image
    return processedImageUrl

// Define a function to notify the user
function notifyUser(userId, processedImageUrl):
    // Create a notification message
    message = "Your image has been processed! View it here: " + processedImageUrl

    // Send notification to the user (e.g., via email or push notification)
    sendNotification(userId, message)

// Main execution flow
function main(event):
    // When an image is uploaded, handle the upload
    handleImageUpload(event)        
```