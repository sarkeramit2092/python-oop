
### 📘 Python OOP: Class Method

In Python's Object-Oriented Programming (OOP), a **class method** is a method that is bound to the class and not the instance of the class. It can only access or modify **class state**.

---

### 🔹 Key Features:
- Defined using the `@classmethod` decorator.
- The first parameter is `cls` (not `self`), referring to the class.
- Can modify class variables shared across all instances.

---

### 🧪 Basic Syntax:
```python
class MyClass:
    class_variable = 0

    @classmethod
    def my_class_method(cls):
        cls.class_variable += 1
```

---

### 🐍 Example Based on Provided Code:

```python
class Bilal:
    count = 0  # Class variable shared across all instances

    def __init__(self, name, age, color):
        self.name = name
        self.age = age
        self.color = color
        Bilal.count += 1  # Increment class variable

    def one_decade_later(self):
        print(f"10 years later, age of {self.name} will be {self.age + 10}")

    #decorator
    @classmethod
    def get_count(cls):
        print(f"Total Bilal instances created: {cls.count}")
```

---

### 🧾 Usage:
```python
b1 = Bilal("Ali", 25, "Brown")
b2 = Bilal("Sara", 30, "Black")

Bilal.get_count()
# Output: Total Bilal instances created: 2
We also can,
b2.get_count()  # same output; as python understood this a part of this class. But as this is the class method, so called this by class name is best practice.
```

---

### ✅ When to Use Class Methods:
- When you need to access or modify class-level data.
- To define factory methods that instantiate the class using different parameters.
