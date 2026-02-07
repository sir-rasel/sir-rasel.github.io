---
title: "Tale of Software Architect(ure): Part 8 (Architecture Patterns and Layered Architecture)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-08T00:00:00Z"
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
    image: "img/blogs/90-software-architecture-layered.png"
    caption: "Layered Architecture"
    alt: "Layered Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 7:** [Tale of Software Architect(ure): Part 7 (Well Known Software Architectures Styles)]({{< ref "blogs/89-software-architecture-patterns.md" >}})
---

{{< figure
    src="/img/blogs/90-software-architecture-layered.png"
    caption="Layered Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the layered software architecture pattern.

So let's get started...

---

## Story:
One day, a customer enters the restaurant. The host greets them and shows them to a table. The waiter arrives, takes their order, and passes it to the chef. The chef checks with the stockroom manager to ensure they have all the ingredients. The stockroom, in turn, regularly orders fresh supplies from the supplier to keep the kitchen well-stocked. The waiter brings the finished meal to the customer, who enjoys a perfect dining experience.

Each person in the restaurant has a clear role. The host doesn’t cook, the waiter doesn’t manage stock, and the chef doesn’t greet customers. Each layer focuses on its own responsibilities, ensuring smooth and efficient operation in a sequential manner.

---

## Architecture Patterns & Its Category:

- ***Patterns***

Architectural patterns are specific, reusable solutions to common architectural problems. Its establishes a relationship between:
1.  **Context**: A recurring, common situation in the world that gives rise to a problem.
2.  **Problem**: The problem, appropriately generalized, that arises in the given context.
3.  **Solution**: A successful architectural resolution to the problem, appropriately abstracted.

- ***Category***
1.  **Module Patterns**: Dominant by the concern of module organization.
2. **Component and Connector (C&C) Patterns**: Dominant by the concern of component and their connectors.
3.  **Allocation Patterns**: Its a mixed, hybrid of previous 2 types.

---

## Similarity and Difference of Architecture Styles and Patterns:
- **Architectural styles** are broad design approaches that define the general structure of a software system (e.g. how components interact).
- **Architectural patterns** are more focused and detailed, offering prescriptive solutions to recurring architectural problems, often within the context of a specific architectural style.

You can think of architecture styles as the big-picture strategy and architecture patterns as detailed tactics used within that strategy.

---

## Layered (N-Tier) Architecture:
{{< figure
    src="/img/blogs/90-layered-architecture.png"
    caption="Layered Architecture (Photo Credit: herbertograca)"
    align=center
>}}

Layered architecture is a software design pattern that structures an application into multiple layers, each with distinct responsibilities. This design promotes separation of concerns, making systems easier to develop, test, and maintain. In a typical layered architecture, each layer only interacts with its adjacent lower layers, creating a clean and manageable structure.

### Context
Layered architecture is commonly applied in building large, scalable, and maintainable software systems that require clear separation between different parts of the system. It is often used in enterprise applications, web systems, and mobile apps, where different components such as user interfaces, business logic, and databases need to work together seamlessly.

In such environments:
- Different teams may be responsible for different layers (e.g., front-end developers for the presentation layer, back-end developers for business logic).
- The system grows over time, making it important to be able to modify or extend parts of the application without disrupting the whole.
- Code needs to be reused across multiple applications, where some systems may use different user interfaces but share business logic or data handling.

### Problem
Without a clear structure, software systems can become giant and hard to manage:
- **Tight coupling**: If all parts of the system are intertwined, changes in one area may have cascading effects, leading to bugs or regressions.
- **Poor separation of concerns**: When business logic, user interfaces, and data management are all mixed, the system becomes harder to maintain, test, and extend.
- **Code duplication**: Different parts of the application may handle similar tasks in different ways, leading to inconsistent behavior and redundant code.
- **Scalability issues**: When the system grows, the lack of modularity makes it harder to scale either the development process or the application performance.

### Solution
The Layered Architecture addresses these problems by breaking the system into distinct layers, each with a clear role:

**Separation of Concerns:**
- Each layer is responsible for a particular aspect of the system, such as handling the user interface, managing business rules, or dealing with data storage.
- This allows developers to focus on one layer at a time without needing to understand the full complexity of the entire system.

**Loose Coupling:**
- By restricting interactions between layers (e.g., the UI only communicates with the business layer, not directly with the data layer), layers are loosely coupled.
- This makes it easier to modify or replace one layer without affecting others.

**Reusability:**
- The business logic layer or data access layer can be reused across multiple applications that share common functionalities but have different user interfaces.
- For example, both a web app and a mobile app can use the same business logic but have different presentation layers.

**Testability:**
- Since each layer has a clear responsibility and only interacts with adjacent layers, testing can be isolated to a single layer.
- Mocking or stubbing out other layers becomes easier, improving the reliability of unit and integration tests.

### Example Solution
In a hotel reservation system:

- **Context:**

The system needs to manage customer reservations, handle payments, provide an interface for guests to browse available rooms, and store booking data in a database.

- **Problem:**

Without clear separation, the code that handles room availability, customer interaction, and payment processing would be mixed together, making it difficult to modify, debug, or scale as the system grows.

- **Layered Solution:**
1.  **Presentation Layer**: A web interface that allows users to search for available rooms, enter booking details, and confirm reservations.
2.  **Application Layer**: Coordinates the reservation process by managing interactions between the UI and the business rules. It validates booking requests, calculates total costs, and ensures rooms are available.
3.  **Business Logic Layer**: Contains rules such as room pricing based on season, availability checks, and customer loyalty program benefits.
4.  **Data Access Layer**: Queries the database for available rooms, customer information, and reservation details, ensuring the data is consistent and properly stored.
5.  **Database Layer**: Stores all hotel data, including room availability, booking records, and payment history in a relational database like MySQL.

By using layered architecture, each part of the system can evolve independently, be tested separately, and scale as needed without affecting other parts of the application.

---

## Pseudocode:

1. Presentation Layer (UI Layer)
```python
function displayAvailableRooms():
    checkInDate = getUserInput("Enter check-in date:")
    checkOutDate = getUserInput("Enter check-out date:")
    
    availableRooms = ReservationService.findAvailableRooms(checkInDate, checkOutDate)
    
    if availableRooms is empty:
        print("No rooms available for the selected dates.")
    else:
        print("Available Rooms: ", availableRooms)
        roomSelection = getUserInput("Select a room:")
        ReservationService.bookRoom(roomSelection, checkInDate, checkOutDate)

function getUserInput(prompt):
    print(prompt)
    return userInput()        
```

2. Application Layer (Service Layer)
```python
class ReservationService:
    
    function findAvailableRooms(checkInDate, checkOutDate):
        return RoomAvailabilityService.getAvailableRooms(checkInDate, checkOutDate)

    function bookRoom(roomId, checkInDate, checkOutDate):
        if RoomAvailabilityService.isRoomAvailable(roomId, checkInDate, checkOutDate):
            totalCost = BookingService.calculateTotalCost(roomId, checkInDate, checkOutDate)
            BookingService.createBooking(roomId, checkInDate, checkOutDate, totalCost)
            print("Room booked successfully!")
        else:
            print("Room is not available for the selected dates.")        
```

3. Business Logic Layer (Domain Layer)
```python
class RoomAvailabilityService:
    
    function getAvailableRooms(checkInDate, checkOutDate):
        return RoomRepository.findAvailableRooms(checkInDate, checkOutDate)

    function isRoomAvailable(roomId, checkInDate, checkOutDate):
        return RoomRepository.isRoomAvailable(roomId, checkInDate, checkOutDate)

class BookingService:
    
    function calculateTotalCost(roomId, checkInDate, checkOutDate):
        room = RoomRepository.getRoomById(roomId)
        numberOfNights = calculateNights(checkInDate, checkOutDate)
        return room.pricePerNight * numberOfNights

    function createBooking(roomId, checkInDate, checkOutDate, totalCost):
        BookingRepository.saveBooking(roomId, checkInDate, checkOutDate, totalCost)        
```

4. Data Access Layer (Persistence Layer)
```python
class RoomRepository:
    
    function findAvailableRooms(checkInDate, checkOutDate):
        query = "SELECT * FROM rooms WHERE room_id NOT IN (SELECT room_id FROM bookings WHERE check_in_date < checkOutDate AND check_out_date > checkInDate)"
        return Database.execute(query)
    
    function isRoomAvailable(roomId, checkInDate, checkOutDate):
        query = "SELECT * FROM rooms WHERE room_id = roomId AND room_id NOT IN (SELECT room_id FROM bookings WHERE check_in_date < checkOutDate AND check_out_date > checkInDate)"
        return Database.execute(query)

    function getRoomById(roomId):
        query = "SELECT * FROM rooms WHERE room_id = roomId"
        return Database.execute(query)

class BookingRepository:
    
    function saveBooking(roomId, checkInDate, checkOutDate, totalCost):
        query = "INSERT INTO bookings (room_id, check_in_date, check_out_date, total_cost) VALUES (roomId, checkInDate, checkOutDate, totalCost)"
        Database.execute(query)        
```

5. Database Layer (Data Storage)
```python
class Database:
    
    function execute(query):
        # Simulated database query execution
        # In a real implementation, this would involve running the query against the database and returning results
        print("Executing query: ", query)
        return result        
```

---

## Summary:
Layered architecture is a software design pattern that organizes an application into distinct layers, each responsible for specific tasks. This separation of concerns makes the system easier to develop, maintain, and scale.

Key Layers:
1.  **Presentation Layer**: Handles user interactions (e.g. web interface, mobile app).
2.  **Application Layer**: Manages the application's operations and flow, coordinating between the layers.
3.  **Business Logic Layer**: Implements the core business rules and decision-making.
4.  **Data Access Layer**: Manages data interactions, such as retrieving and storing data in databases.
5.  **Database Layer**: Stores data persistently (e.g. SQL/NoSQL databases).
