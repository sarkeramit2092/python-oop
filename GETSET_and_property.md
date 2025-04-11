# 🔐 Encapsulation in Python

Encapsulation is one of the fundamental principles of **object-oriented programming (OOP)**. It restricts direct access to some of an object’s components and helps prevent accidental modification of data.

![normally](https://github.com/user-attachments/assets/dba9140e-549f-4a56-a125-e4fe92d6025b)

![with_property_setter](https://github.com/user-attachments/assets/fd7577ad-20dd-46b8-8b38-7a3a410e3611)

![property decorator](https://github.com/user-attachments/assets/87b334b8-1e71-48e2-b061-4a812f07714f)

# Finally 

```python
class BankAccount:
    def __init__(self, account_number, balance):
        self.account_number = account_number
        self.__balance = balance

    def get_balance(self):
        return self.__balance
    
    def set_balance(self, new_balance):
            self.__balance = new_balance


bracbank = BankAccount(243,8000)

print (bracbank.get_balance()) #getter

bracbank.set_balance(12000)    #setter

print (bracbank.get_balance())

print(bracbank.account_number)
```

**But using ```python get_balance()``` -showing people that we are using method "()" to call private variable. So our target is to use private attributes like normal attributes/variables.

![gettersetter](https://github.com/user-attachments/assets/794e5991-3096-4aa3-bbce-8f97a5cd93df)

```python
class BankAccount:
    def __init__(self, account_number, balance):
        self.account_number = account_number
        self.__balance = balance

    @property
    def balance(self):
        return self.__balance

    @balance.setter
    def balance(self, new_balance):    #set_balance to balance because our variable named balance.
            self.__balance = new_balance


bracbank = BankAccount(243,8000)

print (bracbank.balance) #getter

bracbank.balance = 20000   #setter

print (bracbank.balance)

print(bracbank.account_number)
```
**Now bracbank.balance behaves like a normat attribute. But it actually calles the "def balance(sefl):" method.
![method_name_property](https://github.com/user-attachments/assets/aa478006-09a5-420b-a0d8-fa0681334461)


# What is Backward Compatibility?
Backward compatibility means new code changes won't break the existing code that depends on the old behavior.

So, if you had users (or your own codebase) calling a method like:

```python
account.get_balance()
```
And later, you want to make balance look like a normal attribute:

```python

account.balance  # instead of account.get_balance()
```
You want to support both styles (old and new), at least for a while, so that existing code still works — this is backward compatibility.

💡 Using @property for Backward Compatibility
Let’s say you had this original class:

```python

class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance
```

And lots of code is using:

```python

account.get_balance()
Now, you decide to make it cleaner and Pythonic:

python
Copy code
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    @property
    def balance(self):
        return self.__balance
```
But… if you remove get_balance(), all the old code will break.

So, to maintain backward compatibility, you can keep the old method:

```python

class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):             # ✅ Old method still works
        return self.__balance

    @property
    def balance(self):                # ✅ New style also works
        return self.__balance
```

Now both work:

```python
print(account.get_balance())  # Old code
print(account.balance)        # New code
```
✅ Why This Matters
If you're maintaining a library or large codebase, you don't want to break all existing usage when making things cleaner or more modern.

You gradually transition code to the new way without creating bugs or breaking changes.

🧼 Bonus Tip: Mark Deprecated
If you want to encourage users to switch to the new @property, you can show a warning:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        warnings.warn("Use '.balance' instead of 'get_balance()'", DeprecationWarning)
        return self.__balance

    @property
    def balance(self):
        return self.__balance
```
Now when someone uses the old method, they’ll get:

```pgsql
DeprecationWarning: Use '.balance' instead of 'get_balance()'
```


✅ Full Example: With Getter, Setter, and Backward Compatibility

```python

import warnings

class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    # Backward-compatible getter
    def get_balance(self):
        warnings.warn("Use '.balance' instead of 'get_balance()'", DeprecationWarning)
        return self.__balance

    # Backward-compatible setter
    def set_balance(self, new_balance):
        warnings.warn("Use '.balance = value' instead of 'set_balance()'", DeprecationWarning)
        if new_balance < 0:
            raise ValueError("Balance cannot be negative")
        self.__balance = new_balance

    # Modern Pythonic way - property getter
    @property
    def balance(self):
        return self.__balance

    # Modern Pythonic way - property setter
    @balance.setter
    def balance(self, new_balance):
        if new_balance < 0:
            raise ValueError("Balance cannot be negative")
        self.__balance = new_balance
```
🧪 Usage
```python
account = BankAccount(1000)
```
# ✅ New preferred way
```python
print(account.balance)      # Getting balance
account.balance = 5000      # Setting balance
print(account.balance)
```

# 🔁 Old way (still works, but shows warning)
print(account.get_balance())
account.set_balance(9000)
print(account.get_balance())

🔔 Output (with warnings)

5000
9000
<ipython-input-2>:12: DeprecationWarning: Use '.balance' instead of 'get_balance()'
<ipython-input-2>:17: DeprecationWarning: Use '.balance = value' instead of 'set_balance()'

