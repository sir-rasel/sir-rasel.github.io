---
title: "Refactoring - Part 2 (Techniques for Cleaning Up the Smells)"
description: "Let's learn how can we effectively refactor and revamp our codebase"
date: 2025-08-28
tags: ["programming", "refactoring", "revamp-codebase"]
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
    image: "img/blogs/21-refactoring-cleanup-smells.png"
    caption: "clean code"
    alt: "clean code"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Refactoring - Part 1 (Principle, What It Is & Is Not, Identify the Smells First)]({{< ref "blogs/20-refactoring-part-1-principles.md" >}})
---

{{< figure
    src="/img/blogs/21-refactoring-cleanup-smells.png"
    caption="Refactoring Techniques"
    align=center
>}}

In our previous part, we talked about what is refactoring and what is not, the motivation behind this, and identifying the common code smells we generally found in our codebase. In this part we are going to explore some well-known techniques that can help us to clean up the code smells. So let's start...

### Techniques for Cleaning Up the Smells
- **Extract Method:** Move a block of code into a new method with a meaningful name.
> **Before:**
```python
def process_order(order):
    print("Validating...")
    print("Calculating total...")
```
> **After:**
```python
def process_order(order):
    validate_order()
    calculate_total()

def validate_order():
    print("Validating...")

def calculate_total():
    print("Calculating total...")
```

- **Inline Method:** Replace a simple method call with its contents directly in the caller.
> **Before:**
```python
def get_discount(price):
    return calculate_discount(price)

def calculate_discount(price):
    return price * 0.1
```
> **After:**
```python
def get_discount(price):
    return price * 0.1
```

- **Extract Variable:** Create a variable for an expression to make it clearer.
> **Before:**
```python
if order.total_price() > 1000:
    print("High-value order")
```
> **After:**
```python
total = order.total_price()
if total > 1000:
    print("High-value order")
```

- **Inline Variable:** Replace a variable with its value directly in the code.
> **Before:**
```python
discount = order.get_discount()
final_price = price - discount
```
> **After:**
```python
final_price = price - order.get_discount()
```

- **Split Variable:** Use separate variables for different purposes instead of reusing one.
> **Before:**
```python
temp = 5
temp = temp + 10
```
> **After:**
```python
base = 5
result = base + 10
```

- **Rename Variable/Method/Class:** Change the name to make its purpose clearer.
> **Before:**
```python
def calc(x, y):
    return x + y
```
> **After:**
```python
def calculate_sum(first_number, second_number):
    return first_number + second_number
```

- **Replace Nested Conditionals:** Replace complex if-else or switch with simpler methods or polymorphism.
> **Before:**
```python
if user:
    if user.is_active:
        print("Welcome!")
```
> **After:**
```python
if user and user.is_active:
    print("Welcome!")
```

- **Decompose Conditional:** Break down long conditionals into separate methods.
> **Before:**
```python
if user.age > 18 and user.has_license:
    print("Eligible to drive")
```
> **After:**
```python
def is_eligible(user):
    return user.age > 18 and user.has_license

if is_eligible(user):
    print("Eligible to drive")
```

- **Consolidate Duplicate Conditional Fragments:** Combine duplicate logic within conditionals into one place.
> **Before:**
```python
if user.is_admin:
    print("Access granted")
if user.is_manager:
    print("Access granted")
```
> **After:**
```python
if user.is_admin or user.is_manager:
    print("Access granted")
```

- **Replace Magic Numbers:** Replace hardcoded values with constants.
> **Before:**
```python
if account.balance > 100000:
    print("VIP customer")
```
> **After:**
```python
VIP_THRESHOLD = 100000
if account.balance > VIP_THRESHOLD:
    print("VIP customer")
```

- **Simplify Boolean Expressions:** Refactor complex boolean logic into smaller, meaningful expressions.
> **Before:**
```python
if not (user.age < 18):
    print("Adult")
```
> **After:**
```python
if user.age >= 18:
    print("Adult")
```

- **Move Method:** Move a method to a more relevant class.
> **Before:**
```python
class Order:
    def get_customer_email(self, customer):
        return customer.email
```
> **After:**
```python
class Customer:
    def get_email(self):
        return self.email
```

- **Move Field:** Shift a field to a class where it makes more sense.
> **Before:**
```python
class Order:
    def __init__(self):
        self.customer_name = ""
```
> **After:**
```python
class Customer:
    def __init__(self):
        self.name = ""
```

- **Extract Class:** Split a class into two when it does too much.
> **Before:**
```python
class Person:
    def __init__(self, name, street, city):
        self.name = name
        self.street = street
        self.city = city
```
> **After:**
```python
class Person:
    def __init__(self, name, address):
        self.name = name
        self.address = address

class Address:
    def __init__(self, street, city):
        self.street = street
        self.city = city
```

- **Inline Class:** Merge a small, unnecessary class into another.
> **Before:**
```python
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()
```
> **After:**
```python
class Car:
    def start_engine(self):
        print("Engine started")
```

- **Replace Type Code with Class/Enum:** Replace a numeric or string type with a class or enumeration.
> **Before:**
```python
status = "active"
```
> **After:**
```python
from enum import Enum

class Status(Enum):
    ACTIVE = "active"
    INACTIVE = "inactive"
```

- **Replace Delegation with Inheritance:** Use inheritance instead of delegating behavior.
> **Before:**
```python
class Printer:
    def print(self):
        print("Printing...")

class AdvancedPrinter:
    def __init__(self):
        self.printer = Printer()

    def print(self):
        self.printer.print()
```
> **After:**
```python
class AdvancedPrinter(Printer):
    pass
```

- **Parameterize Method:** Replace similar methods with one that uses parameters.
> **Before:**
```python
def add_tax(price):
    return price * 1.1

def add_discount(price):
    return price * 0.9
```
> **After:**
```python
def adjust_price(price, factor):
    return price * factor
```

- **Remove Parameter:** Eliminate unnecessary parameters in a method.
> **Before:**
```python
def greet_user(user, time_of_day):
    if time_of_day:
        print(f"Good {time_of_day}, {user.name}")
    else:
        print(f"Hello, {user.name}")
```
> **After:**
```python
def greet_user(user):
    print(f"Hello, {user.name}")
```

- **Introduce Parameter Object:** Group related parameters into a new object.
> **Before:**
```python
def create_order(customer_name, customer_address):
    pass
```
> **After:**
```python
class Customer:
    def __init__(self, name, address):
        self.name = name
        self.address = address

def create_order(customer):
    pass
```

- **Preserve Whole Object:** Pass an object instead of its individual fields as parameters.
> **Before:**
```python
def display_customer(name, address):
    print(f"Name: {name}, Address: {address}")
```
> **After:**
```python
def display_customer(customer):
    print(f"Name: {customer.name}, Address: {customer.address}")
```

- **Replace Method with Method Object:** Turn a complex method into an object for better organization.
> **Before:**
```python
def calculate():
    pass
```
> **After:**
```python
class Calculator:
    def calculate(self):
        pass
```

- **Encapsulate Field:** Use getter and setter methods for direct field access.
> **Before:**
```python
class User:
    age = 25
```
> **After:**
```python
class User:
    def __init__(self, age):
        self._age = age

    def get_age(self):
        return self._age
```

- **Replace Array with Object:** Use an object to make array data more meaningful.
> **Before:**
```python
student = ["John", 25]
```
> **After:**
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

- **Duplicate Observed Data:** Keep copies of dependent data to reduce dependencies.
> **Before:**
```python
class Product:
    def __init__(self, price):
        self.price = price
    def update_price(self, price):
        self.price = price

class Display:
    def show_price(self, product):
        print(f"Price: {product.price}")
```
> **After:**
```python
class Product:
    def __init__(self, price):
        self._price = price
        self.observers = []

    def update_price(self, price):
        self._price = price
        self.notify_observers()

    def notify_observers(self):
        for observer in self.observers:
            observer.update(self)

class Display:
    def update(self, product):
        self.price = product._price
        print(f"Updated Price: {self.price}")
```

- **Change Bidirectional Association to Unidirectional:** Simplify relationships between classes.
> **Before:**
```python
class Student:
    def __init__(self, name):
        self.name = name
        self.courses = []

class Course:
    def __init__(self, title):
        self.title = title
        self.students = []
```
> **After:**
```python
class Student:
    def __init__(self, name):
        self.name = name
        self.courses = []

class Course:
    def __init__(self, title):
        self.title = title
# Remove bidirectional link; only student knows their courses
```

- **Introduce Null Object:** Replace null with a default object to avoid checks.
> **Before:**
```python
if user is None:
    user = "Guest"
```
> **After:**
```python
class GuestUser:
    name = "Guest"
user = user or GuestUser()
```

- **Replace Conditional with Polymorphism:** Replace conditionals with subclasses or methods for specific behaviors.
> **Before:**
```python
if shape == "circle":
    area = 3.14 * radius ** 2
elif shape == "rectangle":
    area = length * width
```
> **After:**
```python
class Shape:
    def get_area(self):
        pass

class Circle(Shape):
    def get_area(self):
        return 3.14 * radius ** 2

class Rectangle(Shape):
    def get_area(self):
        return length * width
```

- **Replace Constructor with Factory Method:** Use a factory method for creating objects.
> **Before:**
```python
class Car:
    def __init__(self, model, engine_type):
        self.model = model
        self.engine_type = engine_type
```
> **After:**
```python
class Car:
    def __init__(self, model, engine_type):
        self.model = model
        self.engine_type = engine_type

    @staticmethod
    def create_electric_car(model):
        return Car(model, "electric")

    @staticmethod
    def create_gas_car(model):
        return Car(model, "gas")
```

- **Introduce Explaining Variable:** Use variables with descriptive names to clarify logic.
> **Before:**
```python
if (order.total_price() > 1000 and order.customer_age() > 60):
    print("Eligible for senior discount")
```
> **After:**
```python
is_high_value_order = order.total_price() > 1000
is_senior_customer = order.customer_age() > 60

if is_high_value_order and is_senior_customer:
    print("Eligible for senior discount")
```

- **Remove Dead Code:** Delete unused methods or fields.
> **Before:**
```python
def unused_function():
    pass
```
> **After:**
```python
# totally remove the unused code
```

- **Consolidate Duplicate Code:** Merge repeated code into one method.
> **Before:**
```python
if user.is_admin:
    print("Welcome, Admin!")
    log_access("Admin")

if user.is_manager:
    print("Welcome, Manager!")
    log_access("Manager")
```
> **After:**
```python
if user.is_admin or user.is_manager:
    role = "Admin" if user.is_admin else "Manager"
    print(f"Welcome, {role}!")
    log_access(role)
```

- **Replace Inline Code with Function:** Extract repetitive code into reusable functions.
> **Before:**
```python
price_with_tax = price + (price * 0.1)
discounted_price = price - (price * 0.2)
```
> **After:**
```python
def add_tax(price):
    return price + (price * 0.1)

def apply_discount(price):
    return price - (price * 0.2)

price_with_tax = add_tax(price)
discounted_price = apply_discount(price)
```

- **Replace Loop with Pipeline:** Use functional methods like map, filter, or reduce instead of loops.
> **Before:**
```python
squared = []
for num in numbers:
    if num % 2 == 0:
        squared.append(num ** 2)
```
> **After:**
```python
squared = [num ** 2 for num in numbers if num % 2 == 0]
```

- **Split Large Classes:** Break a class into smaller ones for single responsibility.
> **Before:**
```python
class Library:
    def __init__(self):
        self.books = []
        self.members = []

    def add_book(self, book):
        self.books.append(book)

    def add_member(self, member):
        self.members.append(member)

    def issue_book(self, member, book):
        pass

    def calculate_fine(self, member):
        pass
```
> **After:**
```python
class BookCollection:
    def __init__(self):
        self.books = []

    def add_book(self, book):
        self.books.append(book)

class Membership:
    def __init__(self):
        self.members = []

    def add_member(self, member):
        self.members.append(member)
```

---

### References
- Book - Refactoring by Martin Fowler
- Blog - [Refactoring.guru](https://refactoring.guru)