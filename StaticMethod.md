# 🐾 Static Method in Python – Example from the `Bilai` Class

In Python, a `@staticmethod` is a method that belongs to a class but doesn't access or modify class or instance attributes. It's used when a function is logically related to the class but does not depend on its properties.

---

## 🔸 Example: The `Bilai` Class

```python
class Bilai:
    count = 0

    def __init__(self, name, age, color):
        self.name = name
        self.age = age
        self.color = color
        Bilai.count += 1 #Class Attribute

    def name_please(self, x, y):
        print(x,y)
        print(f"My name is {self.name}")

    @classmethod
    def how_many(cls, x, y):
        print(x,y)
        print(f'There are {cls.count} cats')

    @staticmethod
    def addition(x, y):
        print(x,y)
        print("sum=", x + y)


cat2 = Bilai("Lilli",2,"red")

cat2.name_please(5,6) #instance method
Bilai.how_many(5,6)   #class method
Bilai.addition(5,6)   #static method
```
<b><ins>Output</ins></b>
```
5 6
My name is Lilli
5 6
There are 1 cats
5 6
sum= 11
```
✅ Key Characteristics:
Does not use self or cls.

Can be called directly using the class name.

Behaves like a regular function but scoped within the class.

-- You can also call it via an instance, although it's not **recommended**:

``` python
cat = Bilai("Lila", 3, "black")
cat.addition(5, 6)
```

🔍 When to Use @staticmethod
Use it when:

<ins>The logic is related to the class.</ins>

<ins>No need to access or modify class/instance data.</ins>

<ins>You want organizational clarity.</ins>

**🔚 Final Thoughts**
The @staticmethod is perfect for keeping related logic inside a class without coupling it to the instance or the class itself. In the Bilai example, addition() is a clean demonstration of that use case.
