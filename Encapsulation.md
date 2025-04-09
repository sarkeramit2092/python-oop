
# 🔐 Encapsulation in Python

Encapsulation is one of the fundamental principles of **object-oriented programming (OOP)**. It restricts direct access to some of an object’s components and helps prevent accidental modification of data.

![Encapsulation_diagram](https://github.com/user-attachments/assets/da2b28e0-a50e-494d-a1a5-fc5f203ba7dd)

![Encapsulation_diagram_2](https://github.com/user-attachments/assets/a4b82e68-8c01-4e6d-8903-623c2f336103)


---

## ✅ Key Concepts

### 🔐 Public vs Private Variables

```python
class BankAccount:
    def __init__(self, account_number, balance, password):
        self.account_number = account_number    # Public variable
        self.__balance = balance                # Private variable
        self.__password = password              # Private variable
```

- `account_number` is **public**, accessible from outside the class.
- `__balance` and `__password` are **private**, intended to be accessed only within the class.

---

## 🔎 Access Control with Methods

```python
def check_balance(self, password):
    if password == self.__password:
        return f"Your balance is: {self.__balance}"
    else:
        return "Incorrect password! Access denied."
```

![Encapsulation](https://github.com/user-attachments/assets/892b7c95-7ac4-4c80-85f2-24ce01c6a2b8)

> print(account.balance)

![Encapsulation](https://github.com/user-attachments/assets/40c36873-033f-4a44-af32-8063beccf03d)



- This method checks if the entered password matches the stored one before displaying the balance.
- It safely accesses private variables.

---

## ❌ Problem in Original Code

```python
if password == self.password:  # ❌ self.password is not defined
return f"Your balance is: {self.balance}"  # ❌ self.balance is also undefined
```

- These lines incorrectly refer to `self.password` and `self.balance`, which do not exist (they are private as `__password` and `__balance`).

---

## 🧪 External Access and Its Flaw

```python
account = BankAccount("54321", 5000, "asdfg")
account.balance = 15000
print(account.balance)
```

- This **creates a new attribute** `balance` in the `account` object instead of modifying the private `__balance`.
- Bypasses encapsulation – hence not recommended.

---

## ✅ Best Practice: Use Getters/Setters

```python
class BankAccount:
    def get_balance(self, password):
        if password == self.__password:
            return self.__balance
        else:
            return "Access denied"
```
---
This image shows a common misconception when working with private variables in Python.

Here’s what’s going wrong and why:

🔍 Code Review
python
Copy
Edit
account = BankAccount("54321", 5000, "asdfg")

account.__balance = 15000
print(account.check_balance("asdfg"))
print(account.__balance)
🔥 What's Actually Happening?
self.__balance in the class is a private variable, so Python uses name mangling to internally rename it as _BankAccount__balance.

When you write:

python
Copy
Edit
account.__balance = 15000
You’re not modifying the private variable. You are creating a new public variable __balance in the account object.

The check_balance method still uses the original private variable (self.__balance, aka _BankAccount__balance) — which still holds the value 5000.

🧪 Output Explanation
swift
Copy
Edit
Your balance is: $5000
15000
check_balance("asdfg") returns $5000 → from the original __balance.

print(account.__balance) prints 15000 → from the new public __balance.

✅ Fix and Access Private Variables Properly
If you really need to access or change a private variable (not recommended without a setter method), you can use:

python
Copy
Edit
account._BankAccount__balance = 15000
But a better approach is to use getter/setter methods:

python
Copy
Edit
def set_balance(self, new_balance, password):
    if password == self.__password:
        self.__balance = new_balance

## 🎯 Summary

**Encapsulation:**
- Protects data from unauthorized access.
- Encourages use of methods for interacting with data.
- Maintains object integrity and security.


![misconception](https://github.com/user-attachments/assets/fd946419-a53a-4ce4-919f-79b370b213ec)

```python
account = BankAccount("54321", 5000, "asdfg")

account.__balance = 15000
print(account.check_balance("asdfg"))
print(account.__balance)
```

# What's Actually Happening?
self.__balance in the class is a private variable, so Python uses name mangling to internally rename it as _BankAccount__balance.

# When you write:

```python
account.__balance = 15000
```
You’re not modifying the private variable. You are creating a <ins> new public variable __balance </ins> in the account object.

The check_balance method still uses the original private variable (self.__balance, aka _BankAccount__balance) — which still holds the value 5000.

🧪 Output Explanation
Your balance is: $5000
15000
check_balance("asdfg") returns $5000 → from the original __balance.

print(account.__balance) prints 15000 → from the new public __balance.

✅ Fix and Access Private Variables Properly
If you really need to access or change a private variable (not recommended without a setter method), you can use:

```python

account._BankAccount__balance = 15000
But a better approach is to use getter/setter methods:

```
``` python

def set_balance(self, new_balance, password):
    if password == self.__password:
        self.__balance = new_balance
```
