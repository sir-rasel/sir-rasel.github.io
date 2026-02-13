---
title: "Tale of Software Architect(ure): Part 9 (MVC Architecture Pattern)"
description: "Let's learn the software architecture in a nutshell!"
date: "2026-01-09T00:00:00Z"
tags: ["software-architect", "software-architecture", "software-design", "model-view-controller"]
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
    image: "img/blogs/91-software-architecture-mvc.png"
    caption: "MVC Architecture"
    alt: "MVC Architecture"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 8:** [Tale of Software Architect(ure): Part 8 (Architecture Patterns and Layered Architecture)]({{< ref "blogs/90-software-architecture-layered.md" >}})
- **Part 10:** [Tale of Software Architect(ure): Part 10 (Pipe-Filter Architecture)]({{< ref "blogs/92-software-architecture-pipe-filter.md" >}})
---

{{< figure
    src="/img/blogs/91-software-architecture-mvc.png"
    caption="MVC Architecture (Photo Credit: LinkedIn Image)"
    align=center
>}}

In this series, we try to explore the software architecture in a nutshell. We will try to learn the different aspects of software architecture and software architects one by one. In this part, we try to explore the MVC software architecture pattern.

So let's get started...

---

## Story

One day, a customer walked into SweetBites and wanted to order a birthday cake. Here’s what happened:

*   The customer told **Babli** (Controller) they wanted a chocolate cake.
*   Babli passed the order to **Malala** (Model), who gathered the ingredients and baked the cake.
*   Once the cake was ready, **Eti** (View) placed it on the display for the customer to see.
*   Babli confirmed the order and finalized the payment.

Thanks to this *well-organized system*, the bakery ran smoothly every day. Malala could focus on baking, Eti could focus on making things look great for the customers, and Babli made sure everyone was in sync. The customer was happy, and the bakery could easily handle many orders without getting overwhelmed.

* * *

## MVC Architecture Pattern:
{{< figure
    src="/img/blogs/91-mvc-architecture.png"
    caption="MVC Architecture (Photo Credit: Geek for Geeks)"
    align=center
>}}

*MVC (Model-View-Controller)* is a software design pattern that divides an application into three interconnected components called Model, View, Controller. This separation helps manage complexity, promotes modularity, and allows for easier maintenance and scaling.

### 1. Context:

In software development, applications often become complex as they grow. Modern applications need to manage a variety of concerns, such as user interaction, data storage, and business logic. Without proper separation, code can become tangled and difficult to maintain, making it challenging to implement new features or fix bugs. There’s a need for an architectural pattern that organizes code effectively and ensures the separation of different responsibilities.

**Common Contexts:**

*   Web applications (e.g. a blogging platform or an e-commerce site)
*   Desktop or mobile applications that involve complex user interfaces and business logic
*   Applications that need a clear division between how data is managed and how it's presented to the user

### 2. Problem:

As the complexity of applications grows, especially about the complex user interface and view, developers often face issues like:

*   **Tight coupling**: The logic for how data is handled, displayed, and updated gets mixed, making it hard to isolate and maintain.
*   **Poor maintainability**: Small changes in one part of the system can lead to unexpected errors or the need for large rewrites elsewhere.
*   **Lack of scalability**: Adding new features requires modifying large portions of the codebase.
*   **Reusability challenges**: Business logic cannot easily be reused across different parts of the application (e.g. a desktop app might need the same business logic as a web app, but tightly coupled code makes this difficult).

Developers need a way to separate concerns so that each part of the system (data management, UI, and interaction logic) can evolve independently.

### 3. Solution:

The MVC architecture pattern addresses these problems by dividing an application into three distinct components: **Model, View,** and **Controller**. This separation promotes modularity, maintainability, and flexibility. Here's how it works:

1. **Model**: Manages the application's data and business logic. It ensures that data is independent of the UI and handles tasks like retrieving, storing, and manipulating information.

*   *Solution provided*: By isolating data handling and logic in the Model, the rest of the application doesn't need to worry about how data is stored or managed. This makes it easier to adapt or replace the data source (e.g. changing databases) without affecting other parts of the system.

2. **View**: Represents the user interface of the application. It’s responsible for displaying the data from the Model to the user and ensuring a clean presentation.

*   *Solution provided*: By isolating the UI in the View, the application can have multiple views for different devices or interfaces (e.g. web vs. mobile). The View can also easily be updated without affecting the rest of the system.

3. **Controller**: Acts as an intermediary between the View and the Model. It handles user inputs, processes them, and updates the Model or View accordingly.

*   *Solution provided*: The Controller takes responsibility for user interactions and application flow. This separation allows developers to change how input is handled or add new features without affecting the UI (View) or data logic (Model).

### Example Solution:

**Problem**: Users need to submit a new blog post.

**MVC Solution:**

*   **Model**: The Post class handles saving the blog post to the database.
*   **View**: Displays a form for submitting blog posts and, upon submission, shows a success message with the updated list of posts.
*   **Controller**: Processes the form data, uses the Model to store the new post, and then updates the View to reflect the new data.

* * *

### Pseudocode:

1. Model (Data and Business Logic): The Model manages the data. It includes the logic for retrieving and storing blog posts.
```python
Class Post:
    Attributes:
        title
        content

    Method get_all_posts():
        # Logic to retrieve all posts from database or storage
        Return list of posts

    Method save_post(title, content):
        # Logic to save the post to the database or storage
        Create new post object
        Save to storage        
```

2. View (User Interface): The View is responsible for displaying the data to the user. It doesn’t perform any business logic.
```python
Class PostView:
    
    Method display_posts(posts):
        For each post in posts:
            Print post.title
            Print post.content

    Method show_new_post_form():
        Print "Enter Title:"
        Input title
        Print "Enter Content:"
        Input content
        Return title, content

    Method show_success_message():
        Print "Post successfully added!"        
```

3. Controller (Handles User Input and Coordinates Between Model and View): The Controller handles user requests, interacts with the Model to retrieve or modify data, and updates the View.
```python
Class PostController:
    # The Controller interacts with both the Model and the View

    Method display_all_posts():
        posts = Post.get_all_posts()  # Get posts from Model
        PostView.display_posts(posts)  # Pass posts to View for display

    Method add_new_post():
        # Show the form to the user to create a new post
        title, content = PostView.show_new_post_form()

        # Pass the user input to the Model to save the post
        Post.save_post(title, content)

        # After saving, show success message using the View
        PostView.show_success_message()        
```

4. Application Logic (Main Flow): The application flow brings everything together, allowing users to either view existing posts or add new posts.
```python
Class BlogApp:
    
    Method run():
        Print "1. View all posts"
        Print "2. Add new post"
        Input choice

        If choice == 1:
            PostController.display_all_posts()

        Else if choice == 2:
            PostController.add_new_post()

# Entry point of the application
App = BlogApp()
App.run()        
```

* * *

## Summary:
The MVC (Model-View-Controller) architecture pattern is a design framework that separates an application into three interconnected components:
1.  **Model**: Manages the application's data and business logic. It handles data storage, retrieval, and updates, independent of the user interface.
2.  **View**: Represents the user interface (UI). It displays the data from the Model to the user and reflects any changes made but doesn’t alter the data itself.
3.  **Controller**: Acts as a mediator between the Model and the View. It processes user inputs, updates the Model, and then refreshes the View with the new data.

This separation of concerns allows for modularity, making applications easier to maintain, test, and scale. The Model handles the data, the View handles the presentation, and the Controller manages user interactions and application flow.