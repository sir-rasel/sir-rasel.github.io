---
title: "Refactoring - Part 1 (Principle, What It Is & Is Not, Identify the Smells First)"
description: "Let's learn how can we effectively refactor and revamp our codebase"
date: 2025-08-27
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
    image: "img/blogs/20-refactoring-principles.png"
    caption: "clean code"
    alt: "clean code"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 2:** [Refactoring - Part 2 (Techniques for Cleaning Up the Smells)]({{< ref "blogs/21-refactoring-part-2-cleanup-smells.md" >}})
---

{{< figure
    src="/img/blogs/20-refactoring-principles.png"
    caption="Refactoring Principles"
    align=center
>}}

### Main Principle of Refactoring
> The main motivation of refactoring is the Boy Scout rule, which is ***"Keep the camp ground cleaner than you found it."*** In our words, ***"Keep the codebase cleaner and more readable than you found it."***

### Definition
> Refactoring is the process of restructuring existing code to improve its quality (like readability or performance) without altering its external or existing behavior.

### What is Refactoring?
- It’s a cleanup process for code.
- It simplifies complex code, removes redundancies, and organizes it better.
- It just restructures the existing code without adding functionality.
- Example: Renaming variables to meaningful names or breaking a large function into smaller ones.

### What is not Refactoring
- Adding new features.
- Fixing bugs.
- Changing how the program works for the user.
- Writing entirely new code.

### Identify the Code Smells with Example
- **Long Method:** A method that’s too long and hard to understand.
```python
def calculate_total(items):
    total = 0
    for item in items:
        total += item['price'] * item['quantity']
    if total > 100:
        discount = total * 0.1
        total -= discount
    # too much logic here
    print(f"Total: {total}")
```
> **Problem:** Too much logic in one method.

- **Large Class:** A class with too many responsibilities.
```python
class Order:
    def __init__(self):
        self.items = []
        self.customer_name = ""
        self.shipping_address = ""
        self.billing_address = ""

    def calculate_total(self):
        # too much logic here
        pass
```
> **Problem:** Handles too many responsibilities.

- **Primitive Obsession:** Using basic data types instead of objects to represent concepts.
```python
user = {'name': 'John', 'email': 'john@example.com'}
```
> **Problem:** Using a dictionary instead of a User class.

- **Long Parameter List:** A method with too many parameters, making it hard to use.
```python
def create_order(customer_name, customer_email, items, shipping_address, discount_code):
    pass
```
> **Problem:** Too many parameters.

- **Data Clumps:** Data fields that always appear together but aren’t grouped into a class.
```python
def display_shipping_label(name, address, city, state, zip_code):
    pass
```
> **Problem:** Related data not grouped into a class or object.

- **Switch Statements:** Overuse of switch or if-else blocks instead of polymorphism.
```python
def get_discount(type):
    if type == "student":
        return 10
    elif type == "senior":
        return 20
    else:
        return 0
```
> **Problem:** Should use polymorphism instead.

- **Temporary Field:** Fields that are only used in some cases, making the class unclear.
```python
class Order:
    def __init__(self):
        self.discount_code = None  # Only used in special cases
```
> **Problem:** Field not always relevant.

- **Refused Bequest:** A subclass that doesn’t use or need methods from its parent class.
```python
class Animal:
    def eat(self):
        pass

class Dog(Animal):
    def eat(self):  # Dog doesn’t need `eat` but is forced to inherit.
        pass
```
> **Problem:** Subclass doesn't need inherited methods.

- **Alternative Classes with Different Interfaces:** Similar classes with inconsistent method names.
```python
class CSVReader:
    def read_csv(self):
        pass

class JSONReader:
    def parse_json(self):
        pass
```
> **Problem:** Similar functionality but inconsistent method names.

- **Divergent Change:** One class changes for many unrelated reasons.
```python
class Report:
    def generate_pdf(self):
        pass

    def send_email(self):
        pass
```
> **Problem:** One class handles unrelated responsibilities.

- **Shotgun Surgery:** A small change requires editing many parts of the code.
```python
class User:
    def update_email(self, new_email):
        self.email = new_email
        # Also update in many other places
```
> **Problem:** Changes require editing multiple parts of the code.

- **Parallel Inheritance Hierarchies:** Adding a class in one hierarchy forces changes in another.
```python
class Manager:
    pass

class Engineer:
    pass

class ManagerBenefits:
    pass

class EngineerBenefits:
    pass
```
> **Problem:** Adding one class forces a new related class.

- **Comments:** Excessive comments instead of clear code.
```python
# Calculate total price of items
def calculate_total(items):
    total = sum(item['price'] for item in items)
    return total
```
> **Problem:** Comment explains what clear code should do.

- **Duplicate Code:** Identical code in multiple places.
```python
def calculate_shipping(items):
    total = sum(item['price'] for item in items)
    return total * 0.1

def calculate_total(items):
    total = sum(item['price'] for item in items)
    return total
```
> **Problem:** Repeated logic.

- **Lazy Class:** A class that doesn’t do enough to justify its existence.
```python
class Helper:
    def do_nothing(self):
        pass
```
> **Problem:** Class doesn’t justify its existence.

- **Data Class:** A class that only has fields and getter/setter methods.
```python
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price
```
> **Problem:** Only holds data, no behavior.

- **Dead Code:** Unused code that serves no purpose.
```python
def unused_function():
    pass
```
> **Problem:** Code that is never used.

- **Speculative Generality:** Over-engineered code for scenarios that might never happen.
```python
def process(data, extra_callback=None):
    if extra_callback:
        extra_callback(data)
```
> **Problem:** Adding complexity for "future" use.

- **Feature Envy:** A method in one class depends too much on another class.
```python
class Cart:
    def calculate_total(self):
        total = 0
        for item in self.items:
            total += item.get_price()  # Too dependent on `Item`'s details
```
> **Problem:** One class uses another's data too much.

- **Inappropriate Intimacy:** Two classes interact too closely, violating encapsulation.
```python
class Order:
    def __init__(self, user):
        self.user = user

    def get_user_email(self):
        return self.user.email
```
> **Problem:** Accessing private fields of another class.

- **Message Chains:** A long chain of method calls to access an object.
```python
order.customer.get_address().get_city()
```
> **Problem:** Chaining too many calls.

- **Middle Man:** A class that adds no value and simply delegates tasks to another.
```python
class Manager:
    def delegate_task(self, task):
        self.worker.perform_task(task)
```
> **Problem:** Adds no value; just passes calls.

- **Incomplete Library Class:** A library class is missing useful methods, leading to workarounds.
```python
class MathLibrary:
    # Lacks a common method like `square_root`
    pass
```
> **Problem:** Missing useful functionality, requiring workarounds.

- **Hidden Temporal Coupling:** Code that requires methods to be called in a specific order but doesn’t make it clear.
```python
user.set_name("John")
user.save()  # Must follow `set_name`, but not obvious.
```
> **Problem:** Order of calls matters but isn’t clear.

---

### References
- Book - Refactoring by Martin Fowler
- Blog - [Refactoring.guru](https://refactoring.guru)