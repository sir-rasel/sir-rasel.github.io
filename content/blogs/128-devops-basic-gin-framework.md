---
title: "DevOps - Step By Step Learning : Part 5 (Create a REST API Server Using Golang and Gin)"
description: "Let's learn the fundamental DevOps concepts!"
date: "2026-02-17T00:00:00Z"
tags: ["devops" , "golang", "GO", "gin"]
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
    image: "img/blogs/128-devops-basic-gin.jfif"
    caption: "DevOps Basic Gin Framework"
    alt: "DevOps Basic Gin Framework"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 4:** [DevOps - Step By Step Learning : Part 4 (Basic Programming Using Golang)]({{< ref "blogs/127-devops-basic-golang.md" >}})
---

{{< figure
    src="/img/blogs/128-devops-basic-gin.jfif"
    caption="DevOps Basic Gin Framework (Photo Credit: Unsplash)"
    align=center
>}}

## Story:

In the last part, Rasel learned the fundamentals of Golang. Now he was thinking of building something to verify his learnings. He decided to build a ToDo REST API server. It was a straightforward CRUD API application. To do so, he explored the possible framework or library that can help to implement a lightweight and faster API server. After some research, he selected the Gin framework.

* * *

## Build REST API Server Using Gin:

For any REST API application some important things need to handle are:

1.  Endpoint design with proper HTTP method.
2.  Security handling (like authentication, authorization, CORS etc)
3.  Route handling and grouping.
4.  Handler or Service design.
5.  Data layer or Repository management.
6.  Data storage, ORM or Database management.

For simplicity we just implement CRUD endpoint and simple data storage without any security handling.

### Step 1: Set up PostgreSQL

Make sure you have PostgreSQL installed and running. You can use Docker or install it locally. Then, create a database named todoapp.

```sql
CREATE DATABASE todoapp;
```

### Step 2: Install dependencies

Run the following commands to install necessary dependencies:

```go
go mod init todoginapi
go get github.com/gin-gonic/gin
go get github.com/jinzhu/gorm
go get github.com/jinzhu/gorm/dialects/postgres        
```

## Step 3: Create the main.go file

Create a file main.go to set up the Gin server and routes.

```go
package main

import (
	"github.com/gin-gonic/gin"
	"github.com/jinzhu/gorm"
	_ "github.com/jinzhu/gorm/dialects/postgres"
	"log"
	"net/http"
	"os"
)

var db *gorm.DB
var err error

func init() {
	// Set up PostgreSQL connection
	dsn := "host=localhost user=yourusername password=yourpassword dbname=todoapp port=5432 sslmode=disable"
	db, err = gorm.Open("postgres", dsn)
	if err != nil {
		log.Fatalf("Failed to connect to database: %v", err)
	}

	// Migrate the schema
	db.AutoMigrate(&Todo{})
}

type Todo struct {
	ID        uint   `json:"id"`
	Title     string `json:"title"`
	Completed bool   `json:"completed"`
}

func main() {
	r := gin.Default()

	// Define routes
	r.GET("/todos", GetTodos)
	r.GET("/todos/:id", GetTodo)
	r.POST("/todos", CreateTodo)
	r.PUT("/todos/:id", UpdateTodo)
	r.DELETE("/todos/:id", DeleteTodo)

	// Run the server
	r.Run(":8080")
}

func GetTodos(c *gin.Context) {
	var todos []Todo
	if err := db.Find(&todos).Error; err != nil {
		c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error()})
		return
	}
	c.JSON(http.StatusOK, todos)
}

func GetTodo(c *gin.Context) {
	id := c.Param("id")
	var todo Todo
	if err := db.First(&todo, id).Error; err != nil {
		c.JSON(http.StatusNotFound, gin.H{"error": "Todo not found"})
		return
	}
	c.JSON(http.StatusOK, todo)
}

func CreateTodo(c *gin.Context) {
	var todo Todo
	if err := c.ShouldBindJSON(&todo); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		return
	}

	if err := db.Create(&todo).Error; err != nil {
		c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error()})
		return
	}
	c.JSON(http.StatusCreated, todo)
}

func UpdateTodo(c *gin.Context) {
	id := c.Param("id")
	var todo Todo
	if err := db.First(&todo, id).Error; err != nil {
		c.JSON(http.StatusNotFound, gin.H{"error": "Todo not found"})
		return
	}

	var updatedTodo Todo
	if err := c.ShouldBindJSON(&updatedTodo); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		return
	}

	todo.Title = updatedTodo.Title
	todo.Completed = updatedTodo.Completed
	if err := db.Save(&todo).Error; err != nil {
		c.JSON(http.StatusInternalServerError, gin.H{"error": err.Error()})
		return
	}

	c.JSON(http.StatusOK, todo)
}

func DeleteTodo(c *gin.Context) {
	id := c.Param("id")
	if err := db.Delete(&Todo{}, id).Error; err != nil {
		c.JSON(http.StatusNotFound, gin.H{"error": "Todo not found"})
		return
	}
	c.JSON(http.StatusOK, gin.H{"message": "Todo deleted successfully"})
}        
```

### Step 4: models.go (Optional)

To structure your code better, you can separate the database logic into its own file models.go.

```go
package main

import (
	"github.com/jinzhu/gorm"
)

type Todo struct {
	ID        uint   `json:"id"`
	Title     string `json:"title"`
	Completed bool   `json:"completed"`
}

func (todo *Todo) Create(db *gorm.DB) (*Todo, error) {
	err := db.Create(todo).Error
	if err != nil {
		return nil, err
	}
	return todo, nil
}

func GetAllTodos(db *gorm.DB) ([]Todo, error) {
	var todos []Todo
	err := db.Find(&todos).Error
	return todos, err
}

func GetTodoByID(db *gorm.DB, id string) (*Todo, error) {
	var todo Todo
	err := db.First(&todo, id).Error
	if err != nil {
		return nil, err
	}
	return &todo, nil
}

func UpdateTodoByID(db *gorm.DB, id string, todo *Todo) (*Todo, error) {
	var existingTodo Todo
	err := db.First(&existingTodo, id).Error
	if err != nil {
		return nil, err
	}
	existingTodo.Title = todo.Title
	existingTodo.Completed = todo.Completed
	db.Save(&existingTodo)
	return &existingTodo, nil
}

func DeleteTodoByID(db *gorm.DB, id string) error {
	return db.Delete(&Todo{}, id).Error
}        
```

### Step 5: Run the server

Now, run the server with:
```bash
go run main.go
```

The server will start at `http://localhost:8080`, and you can test your ToDo CRUD operations with tools like Postman or CURL.

### Testing the endpoints

Create a new ToDo:

*   `POST /todos`
*   Body (JSON):

```json
{
  "title": "Learn Golang",
  "completed": false
}        
```

Get all ToDos:

*   `GET /todos`

Get a single ToDo by ID:

*   `GET /todos/:id`

Update a ToDo:

*   `PUT /todos/:id`
*   Body (JSON):

```json
{
  "title": "Learn Golang and PostgreSQL",
  "completed": true
}        
```

Delete a ToDo:

*   `DELETE /todos/:id`

* * *

## Summary:

This project is a ToDo CRUD REST API built using **Golang**, **Gin**, and **PostgreSQL**. It utilizes the Gin framework for efficient HTTP request handling and **GORM** as an ORM for database interactions. The API connects to a PostgreSQL database, with automatic schema migration handled by GORM. The API accepts and returns JSON data, using gin.Context to process requests and responses. PostgreSQL is connected using GORM's PostgreSQL dialect, with database credentials configured via a DSN string. The application is structured for modularity, with separate concerns for routing, models, and database logic. To run the server, PostgreSQL must be set up, dependencies installed, and the main.go file executed with `go run main.go`.