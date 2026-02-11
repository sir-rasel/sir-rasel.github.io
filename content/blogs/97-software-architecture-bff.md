---
title: "Tale of Software Architect(ure): Part 15 (Backend for Frontend (BFF) Architecture Pattern)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-15T00:00:00Z"
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
    image: "img/blogs/97-software-architecture-bff.png"
    caption: "Backend for Frontend Architecture"
    alt: "Backend for Frontend Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 14:** [Tale of Software Architect(ure): Part 14 (Modular Monolith Architecture Pattern)]({{< ref "blogs/96-software-architecture-modular-monolith.md" >}})
- **Part 16:** [Tale of Software Architect(ure): Part 16 (Domain Driven Design)]({{< ref "blogs/98-software-architecture-ddd.md" >}})
---

{{< figure
    src="/img/blogs/97-software-architecture-bff.png"
    caption="Backend for Frontend Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the backend for frontend architecture pattern.

So let's get started...

---

## Story:

In the land of **AppVille**, there lived two very different characters: **Mobi**, the energetic mobile **app**, and **Webby**, the sophisticated web app. Both served the people of AppVille by connecting them to the **Kingdom of Data**, a realm where all the important information, user profiles, posts, and notifications was stored.

At first, Mobi and Webby relied on the same Royal Backend, a single source of truth for all things data. But there was a problem. The Royal Backend wasn’t tailored for either of them. It treated Mobi and Webby the same, sending them the same information in the same way. This caused a lot of frustration.

One day, the Wise Architect of AppVille realized this wasn’t working. “Mobi and Webby are too different,” the Architect said. “They need their own companions who understand their unique needs.” And so, the BFFs (Backend for Frontend) were born.

Now, whenever Mobi or Webby needed something from the Kingdom of Data, they didn’t go directly to the Royal Backend anymore. They asked their trusted BFFs. With the help of their BFFs, Mobi and Webby thrived. And so, Mobi, Webby, and their BFFs lived happily.

* * *

## Backend for Frontend (BFF) Architecture Pattern:
{{< figure
    src="/img/blogs/97-bff-architecture.png"
    caption="Backend for Frontend Architecture (Photo Credit: LinkedIn)"
    align=center
>}}

Backend for Frontend (BFF) architecture is a design pattern in which separate backend services are created specifically to serve the needs of different frontend applications (e.g., mobile apps, web apps, etc.). Instead of having a single, monolithic backend that tries to serve all kinds of clients, each frontend has its own tailored backend service, allowing for better optimization and separation of concerns. This pattern is useful when you want to avoid customizing a single backend for multiple interfaces. This pattern was first described by Sam Newman.

Key Components of BFF Architecture:

1.  **Frontend Applications**: These are the clients that consume the BFF service. They could be web browsers, mobile apps, or other user interfaces.
2.  **BFF (Backend for Frontend)**: This is the intermediary between the frontend and the core backend services or APIs. It performs tasks like data aggregation, business logic specific to the frontend, authentication, and security. Each frontend might have its own BFF.
3.  **Core Backend Services**: These are the actual services that contain the business logic and data processing. They remain independent of the frontend’s structure, focusing on core functions.

Why BFF is Useful?

*   **Frontend-Specific Optimization**: Each frontend has its own user experience (UX) needs. A mobile app might need less data with more compression compared to a web app. With BFF, these needs can be met separately.
*   **Decoupling Frontend and Backend**: Frontend developers don’t need to worry about changing the entire backend when making frontend-specific changes.
*   **Improved Developer Velocity**: Different teams can work independently on their BFFs, speeding up development.

**Practical Example:**

Let’s say we’re building a social media platform with both a mobile app and a web app. Here’s how the BFF architecture might work:

1. **Web App BFF**

*   The web app BFF may focus on delivering large amounts of data, rich with images and videos, since the web app can handle heavier payloads. It could interact with core services like the user database, post-service, and messaging API to fetch data.
*   The BFF aggregates this information into a single response that fits the web app’s needs and handles browser-based authentication like sessions or cookies.

2. **Mobile App BFF**

*   The mobile app BFF, in contrast, might need to send lightweight responses due to the constraints of mobile networks. It could fetch only the essential data (like text, small images, or thumbnails) to improve performance and optimize for lower bandwidth.
*   It may also handle push notifications, mobile authentication (like OAuth2 tokens), and background sync operations.

* * *

## Context:

In modern software systems, multiple frontend applications often interact with the same backend services. These frontends can include: **Web applications** (desktop browsers), **Mobile applications** (iOS, Android), **Other clients** (e.g., IoT devices, smartwatches)

Each frontend typically has unique requirements, such as:

*   Different data formats and structures
*   Varying performance expectations (e.g., mobile apps may need smaller payloads)
*   Frontend-specific business logic (e.g., displaying data differently or performing specific tasks on behalf of the frontend)

In a traditional **monolithic backend** or a common API shared by all frontends, the backend may struggle to serve the unique needs of each frontend effectively. This often leads to:

*   Over fetching or under fetching of data (inefficient data retrieval)
*   Complex client-side logic to manipulate data, harming performance and user experience
*   Difficulty in maintaining and scaling the backend as more frontends are introduced

## Problem:

A shared, one-size-fits-all backend architecture results in challenges such as:

*   **Inefficient client communication**: Different frontends may receive more data than they need or the wrong data format, requiring additional processing on the client side.
*   **Poor performance**: Mobile applications, for example, may suffer from slow response times or excessive data transfer, impacting user experience.
*   **Tight coupling of frontend and backend**: Frontend changes often require backend adjustments, leading to slower development cycles and increased complexity in maintaining the system.
*   **Difficult to scale**: As the number of frontend types grows (e.g., adding a new smartwatch app), the backend code becomes cluttered with conditional logic to serve different clients, which can lead to performance bottlenecks and maintenance issues.

## Solution:

The Backend for Frontend (BFF) design pattern addresses the problem by introducing custom backends for each frontend type. Each frontend (e.g., web app, mobile app) interacts with its own tailored backend service, which is responsible for aggregating data, handling business logic, and optimizing performance specific to that frontend’s needs.

How the BFF architecture solves the problem?

*   **Frontend-Specific Optimization**: Each BFF is designed to handle the specific needs of a given frontend. For example, a mobile BFF can minimize the amount of data sent to mobile devices and optimize responses for low-latency connections.
*   **Separation of Concerns**: The BFF abstracts frontend-specific logic, ensuring that the core backend services remain focused on business logic without being overloaded with frontend concerns.
*   **Improved Maintainability**: Changes in frontend functionality (e.g., adding new features to the mobile app) can be handled in the respective BFF without modifying the core backend or impacting other frontends.
*   **Scalability**: As new frontends (e.g., smartwatches or new mobile platforms) are introduced, a new BFF can be created for each, without altering the core backend services. This reduces the risk of introducing bugs and simplifies system scaling.

* * *

## Sample Pseudocode:

Here’s a sample pseudocode example illustrating the Backend for Frontend (BFF) architecture for a social media platform with separate BFFs for a mobile app and a web app.

**Scenario:**

*   The core backend provides user data, posts, and notifications through microservices.
*   The mobile app BFF optimizes data for mobile performance (e.g., smaller images, fewer details).
*   The web app BFF provides richer content with more detailed responses.

Core Backend Microservices

*   UserService: Provides user details.
*   PostService: Provides posts from the user’s feed.
*   NotificationService: Fetches unread notifications.

1. **Core Backend Microservices**

```python
class UserService:
    def getUserDetails(userId):
        # Fetch user details from database
        return {
            "id": userId,
            "name": "Alice",
            "profilePicture": "high_res_image.jpg",
            "bio": "Avid photographer and traveler",
            "followers": 1200
        }

class PostService:
    def getUserFeed(userId):
        # Fetch user's posts from database
        return [
            { "postId": 1, "content": "Check out my new photo!", "image": "high_res_photo1.jpg" },
            { "postId": 2, "content": "Exploring the mountains!", "image": "high_res_photo2.jpg" }
        ]

class NotificationService:
    def getUnreadNotifications(userId):
        # Fetch unread notifications for the user
        return [
            { "notificationId": 101, "message": "New follower: John" },
            { "notificationId": 102, "message": "Your post got 20 likes!" }
        ]        
```

2. **Mobile App BFF**

The mobile BFF fetches lightweight data (e.g., smaller images, fewer details) to optimize for mobile performance.

```python
class MobileAppBFF:
    def getMobileUserProfile(userId):
        userDetails = UserService.getUserDetails(userId)
        userFeed = PostService.getUserFeed(userId)
        notifications = NotificationService.getUnreadNotifications(userId)
        
        # Modify user details for mobile (e.g., compress image, reduce bio length)
        userDetails["profilePicture"] = compressImage(userDetails["profilePicture"])
        userDetails["bio"] = truncate(userDetails["bio"], 50)
        
        # Modify feed for mobile (e.g., use thumbnails instead of full images)
        for post in userFeed:
            post["image"] = createThumbnail(post["image"])
        
        # Return the optimized data for the mobile app
        return {
            "user": {
                "id": userDetails["id"],
                "name": userDetails["name"],
                "profilePicture": userDetails["profilePicture"],
                "bio": userDetails["bio"]
            },
            "feed": userFeed,
            "notifications": notifications
        }

    def compressImage(imageUrl):
        # Logic to compress image for mobile
        return "compressed_" + imageUrl

    def createThumbnail(imageUrl):
        # Logic to create thumbnail for mobile
        return "thumbnail_" + imageUrl

    def truncate(text, length):
        # Truncate text to a specific length
        return text[:length] + "..."        
```

3. **Web App BFF**

The web BFF fetches richer content and larger images, as the web app can handle more detailed information.

```python
class WebAppBFF:
    def getWebUserProfile(userId):
        userDetails = UserService.getUserDetails(userId)
        userFeed = PostService.getUserFeed(userId)
        notifications = NotificationService.getUnreadNotifications(userId)
        
        # Return full-size images and complete user data
        return {
            "user": {
                "id": userDetails["id"],
                "name": userDetails["name"],
                "profilePicture": userDetails["profilePicture"],  # Full-size image
                "bio": userDetails["bio"],                        # Full bio
                "followers": userDetails["followers"]
            },
            "feed": userFeed,                                     # Full-size images in posts
            "notifications": notifications
        }        
```

Sample API Response:

1. **Mobile App Response (via MobileAppBFF)**

```json
{
    "user": {
        "id": 1,
        "name": "Alice",
        "profilePicture": "compressed_high_res_image.jpg",
        "bio": "Avid photographer..."
    },
    "feed": [
        { "postId": 1, "content": "Check out my new photo!", "image": "thumbnail_high_res_photo1.jpg" },
        { "postId": 2, "content": "Exploring the mountains!", "image": "thumbnail_high_res_photo2.jpg" }
    ],
    "notifications": [
        { "notificationId": 101, "message": "New follower: John" },
        { "notificationId": 102, "message": "Your post got 20 likes!" }
    ]
}        
```


2. **Web App Response (via WebAppBFF)**

```json
{
    "user": {
        "id": 1,
        "name": "Alice",
        "profilePicture": "high_res_image.jpg",
        "bio": "Avid photographer and traveler",
        "followers": 1200
    },
    "feed": [
        { "postId": 1, "content": "Check out my new photo!", "image": "high_res_photo1.jpg" },
        { "postId": 2, "content": "Exploring the mountains!", "image": "high_res_photo2.jpg" }
    ],
    "notifications": [
        { "notificationId": 101, "message": "New follower: John" },
        { "notificationId": 102, "message": "Your post got 20 likes!" }
    ]
}        
```

* * *

## Summary:

Backend for Frontend (BFF) architecture is a design pattern where separate backend services (BFFs) are created for different frontend applications (e.g., mobile apps, web apps). Each BFF is tailored to meet the specific needs of its corresponding frontend, optimizing data handling, performance, and user experience.

It gives you: Frontend-Specific Backends, Optimized Performance, Decoupling, Improved Scalability etc.

By separating backends for each frontend, the BFF architecture allows for more efficient, flexible, and maintainable systems.