# 🐾 Abstract Methods in Python (With Animals Example)

In object-oriented programming, **abstract methods** are methods that are declared in a base class but must be implemented by all subclasses. This helps enforce a **consistent interface** across classes.

## 🧠 Why Use Abstract Methods?

- Enforces a consistent method name across all subclasses
- Helps organize code and ensure each class implements required functionality
- Enables **polymorphism**

---

## 💡 How to Use Abstract Classes in Python

Python provides the `abc` module (`Abstract Base Classes`) to implement this feature.

### 📄 Code Example:

![without_abstract](https://github.com/user-attachments/assets/7f6bfb8b-20f5-42af-8e05-99a8d40e6229)


```python
from abc import ABC, abstractmethod

# Abstract Base Class
class Animal(ABC):
    @abstractmethod
    def legs(self):
        pass

# Concrete Classes
class Cow(Animal):  # 🐄🐄🐄
    def legs(self):
        print("Cows have 4 legs")

class Ant(Animal):  # 🐜🐜
    def legs(self):
        print("Ants have 6 legs")

class Spider(Animal):  # 🕷🕸🕷
    def legs(self):
        print("Spiders have 8 legs")
```
🧪 Creating and Using Objects

```python
# Creating objects
mr_goru = Cow()
ms_pipra = Ant()
mr_makorsha = Spider()
```
# Polymorphism in action
```python
for animal in [mr_goru, ms_pipra, mr_makorsha]:
    animal.legs()
```
✅ Output

Cows have 4 legs
Ants have 6 legs
Spiders have 8 legs

![abstract_1](https://github.com/user-attachments/assets/087499f3-63cd-4542-978e-e4a3ee24cb71)
![abstract_error](https://github.com/user-attachments/assets/636e5124-8e10-4a74-9e2c-c6cbf3d54997)

# Abstract class does not create any object.

🔚 Summary

ABC	Abstract Base Class
@abstractmethod	Marks a method that must be implemented in child classes
Polymorphism	You can call legs() on any Animal object without knowing its exact class
Using abstract methods makes your code more structured, reusable, and maintainable. 🧑‍💻
