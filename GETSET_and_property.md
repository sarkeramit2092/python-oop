# 🔐 Encapsulation in Python

Encapsulation is one of the fundamental principles of **object-oriented programming (OOP)**. It restricts direct access to some of an object’s components and helps prevent accidental modification of data.

![normally](https://github.com/user-attachments/assets/dba9140e-549f-4a56-a125-e4fe92d6025b)

![with_property_setter](https://github.com/user-attachments/assets/fd7577ad-20dd-46b8-8b38-7a3a410e3611)

![property decorator](https://github.com/user-attachments/assets/87b334b8-1e71-48e2-b061-4a812f07714f)

## ✅ Key Concepts

### 🔐 Public vs Private Variables

```python
class BankAccount:
    def __init__(self, account_number, balance, password):
        self.account_number = account_number    # Public variable
        self.__balance = balance                # Private variable
        self.__password = password              # Private variable
```
account_number is public, accessible from outside the class.
__balance and __password are private, intended to be accessed only within the class.

🔎 Access Control with Methods
```python
def check_balance(self, password):
    if password == self.__password:
        return f"Your balance is: {self.__balance}"
    else:
        return "Incorrect password! Access denied."
```
This method checks if the entered password matches the stored one before displaying the balance.

It safely accesses private variables.

❌ Problem in Original Code

```python
if password == self.password:  # ❌ self.password is not defined
    return f"Your balance is: {self.balance}"  # ❌ self.balance is also undefined
These lines incorrectly refer to self.password and self.balance, which do not exist (they are private as __password and __balance).
```
🧪 External Access and Its Flaw

```python
account = BankAccount("54321", 5000, "asdfg")
account.balance = 15000
print(account.balance)
This creates a new attribute balance in the account object instead of modifying the private __balance.
```
Bypasses encapsulation – hence not recommended.

✅ Best Practice: Use Getters/Setters

```python
class BankAccount:
    def get_balance(self, password):
        if password == self.__password:
            return self.__balance
        else:
            return "Access denied"
```
Encapsulation encourages the use of methods to access or modify internal data securely.

⚠️ Name Mangling and Misleading Access
In Python, private variables (with double underscores) are name-mangled. This means:

```python
self.__balance
```
Is internally stored as:

```python
self._BankAccount__balance
```
❌ Misleading Code

```python
account = BankAccount("54321", 5000, "asdfg")

account.__balance = 15000
print(account.check_balance("asdfg"))
print(account.__balance)
```
🧪 Output
Your balance is: $5000
15000
account.__balance = 15000 creates a new variable.

It does not change the private __balance from within the class.

check_balance() still uses the original private value: 5000.

✅ Correct Way (Not Recommended, but for Learning)

```python
account._BankAccount__balance = 15000
```
This directly accesses the private field using the name-mangled format.

🛡 Best Practice: Use Setters

```python
def set_balance(self, new_balance, password):
    if password == self.__password:
        self.__balance = new_balance
```
### Using @property for Getters and Setters
Python provides a neat way to encapsulate data with the @property decorator. This lets you control access to private attributes in a clean, readable way.

✅ Example: Getter and Setter
```python
class BankAccount:
    def __init__(self, account_number, balance, password):
        self.account_number = account_number
        self.__balance = balance
        self.__password = password

    @property
    def balance(self):
        return self.__balance

    @balance.setter
    def balance(self, value):
        if value >= 0:
            self.__balance = value
        else:
            raise ValueError("Balance cannot be negative")
```
🔎 Usage

```python
account = BankAccount("54321", 5000, "asdfg")

print(account.balance)     # ➡ Calls the getter
account.balance = 7000     # ➡ Calls the setter

print(account.balance)     # ➡ Shows updated value: 7000
```
You interact with the balance attribute directly, but it's actually using methods under the hood.

❌ Without Setter
If you only define @property:

```python
@property
def balance(self):
    return self.__balance
```
Trying to set account.balance = 1000 will raise:

AttributeError: can't set attribute

🔐 Optional: Setter with Password Check
For secure updates:

```python
def set_balance(self, value, password):
    if password == self.__password:
        self.__balance = value
    else:
        print("Unauthorized access!")
```
While this can't use the @balance.setter decorator directly (since decorators don’t support multiple arguments like passwords), it's useful for custom security logic.


