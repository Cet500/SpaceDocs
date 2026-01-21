# 3.2 Классы: Группируй код в объекты

## Введение: Когда функций становится много

Представь, у тебя есть функции для работы с пользователем:

```python
def create_user(name, email):
    return {"name": name, "email": email}

def get_user_name(user):
    return user["name"]

def get_user_email(user):
    return user["email"]

def set_user_email(user, email):
    user["email"] = email
```

Это работает, но **разбросано**. Было бы лучше собрать всё про пользователя в одно место:

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email
    
    def get_name(self):
        return self.name
    
    def change_email(self, email):
        self.email = email
```

Это **класс** — группировка данных и функций в одном объекте.

**В этой главе:**

1. Что такое класс (просто!)
2. Как создавать объекты (instance)
3. Методы и атрибуты (данные и функции)
4. Инициализация (`__init__`)

**Результат:** Твой код будет **организованнее и логичнее**. 🎯

---

## Живой пример: Класс вместо функций

**Без класса (раскидано):**

```python
user1_name = "Миша"
user1_email = "misha@mail.com"
user1_age = 25

user2_name = "Анна"
user2_email = "anna@mail.com"
user2_age = 23
```

**С классом (организовано):**

```python
class User:
    def __init__(self, name, email, age):
        self.name = name
        self.email = email
        self.age = age

user1 = User("Миша", "misha@mail.com", 25)
user2 = User("Анна", "anna@mail.com", 23)

print(user1.name)   # Миша
print(user2.email)  # anna@mail.com
```

**Видишь?** С классом код **чище и понятнее**! 📦

---

## Что такое класс? (Просто)

**Класс** — это чертёж для создания объектов.

**Аналогия:**

- 📋 Класс = чертёж дома
- 🏠 Объект = построенный дом

Один чертёж может создать много домов, но все они построены по одному плану.

---

## Синтаксис: Как писать класс

```python
class ClassName:          # Объявление класса
    def __init__(self, param):  # Инициализация (конструктор)
        self.param = param  # Атрибут (данные)
    
    def method(self):     # Метод (функция)
        return self.param
```

**Части:**

- `class` — ключевое слово
- `ClassName` — имя класса (заглавными буквами!)
- `__init__` — метод инициализации (вызывается при создании объекта)
- `self` — "я сам" (ссылка на текущий объект)

---

## Пример 1: Простой класс

```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def bark(self):
        return f"{self.name} лает: Гав!"
    
    def get_age(self):
        return self.age

# Создаём объекты
dog1 = Dog("Шарик", 3)
dog2 = Dog("Бобик", 5)

# Используем
print(dog1.name)      # Шарик
print(dog1.bark())    # Шарик лает: Гав!
print(dog2.get_age()) # 5
```

**Разбор:**

- `dog1 = Dog("Шарик", 3)` — создание объекта (экземпляра класса)
- `dog1.name` — атрибут (данные)
- `dog1.bark()` — метод (функция)

---

## Пример 2: Класс для задачи

```python
class Task:
    def __init__(self, title, priority=1):
        self.title = title
        self.priority = priority
        self.completed = False
    
    def mark_completed(self):
        self.completed = True
    
    def get_status(self):
        status = "✓" if self.completed else "○"
        return f"{status} {self.title} (приоритет: {self.priority})"

# Использование
task1 = Task("Купить продукты", 1)
task2 = Task("Написать отчёт", 2)

print(task1.get_status())  # ○ Купить продукты (приоритет: 1)

task1.mark_completed()
print(task1.get_status())  # ✓ Купить продукты (приоритет: 1)
```

---

## Пример 3: Класс с методами изменения

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance
    
    def deposit(self, amount):
        """Положить деньги"""
        self.balance += amount
        return f"Добавлено {amount}. Баланс: {self.balance}"
    
    def withdraw(self, amount):
        """Снять деньги"""
        if amount > self.balance:
            return "Недостаточно средств!"
        self.balance -= amount
        return f"Снято {amount}. Баланс: {self.balance}"
    
    def get_balance(self):
        """Получить баланс"""
        return f"Счёт {self.owner}: {self.balance} руб."

# Использование
account = BankAccount("Иван", 1000)
print(account.get_balance())    # Счёт Иван: 1000 руб.
print(account.deposit(500))     # Добавлено 500. Баланс: 1500
print(account.withdraw(200))    # Снято 200. Баланс: 1300
print(account.withdraw(2000))   # Недостаточно средств!
```

---

## Понимаем `self`

`self` — это **"я сам"** (текущий объект).

```python
class Person:
    def __init__(self, name):
        self.name = name  # Сохраняю себе имя
    
    def greet(self):
        # self позволяет обратиться к моему имени
        return f"Привет, я {self.name}"

p1 = Person("Миша")
p2 = Person("Анна")

print(p1.greet())  # Привет, я Миша
print(p2.greet())  # Привет, я Анна
```

Каждый объект помнит свои данные через `self`.

---

## Практика: Пишем классы

### Практика 1: Класс Student

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade
        self.grades = []
    
    def add_grade(self, grade):
        """Добавить оценку"""
        self.grades.append(grade)
    
    def get_average(self):
        """Получить среднюю оценку"""
        if not self.grades:
            return 0
        return sum(self.grades) / len(self.grades)
    
    def get_info(self):
        """Информация об ученике"""
        avg = self.get_average()
        return f"{self.name} ({self.grade} класс): средняя {avg:.1f}"

# Использование
student = Student("Анна", 10)
student.add_grade(5)
student.add_grade(4)
student.add_grade(5)

print(student.get_info())  # Анна (10 класс): средняя 4.7
```

---

### Практика 2: Класс Product (товар в магазине)

```python
class Product:
    def __init__(self, name, price, quantity=0):
        self.name = name
        self.price = price
        self.quantity = quantity
    
    def add_stock(self, count):
        """Добавить товар на склад"""
        self.quantity += count
    
    def sell(self, count):
        """Продать товар"""
        if count > self.quantity:
            return f"Ошибка: в наличии только {self.quantity}"
        self.quantity -= count
        return f"Продано {count} шт. {self.name}"
    
    def get_info(self):
        """Информация о товаре"""
        total = self.price * self.quantity
        return f"{self.name}: {self.price} руб. (в наличии: {self.quantity}, сумма: {total} руб.)"

# Использование
apple = Product("Яблоко", 30, 10)
print(apple.get_info())        # Яблоко: 30 руб. (в наличии: 10, сумма: 300 руб.)
print(apple.sell(3))           # Продано 3 шт. Яблоко
print(apple.get_info())        # Яблоко: 30 руб. (в наличии: 7, сумма: 210 руб.)
```

---

## Вопросы для самопроверки

1. **Что такое класс и объект?**

2. **Для чего нужен `self`?**

3. **Что такое `__init__` и когда он вызывается?**

4. **Какая разница между атрибутом и методом?**

5. **Как создать объект класса?**

---

## Практическое задание

### Задание: Класс для банковского счёта (расширенный)

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance
        self.transactions = []
    
    def deposit(self, amount):
        """Положить деньги"""
        self.balance += amount
        self.transactions.append(f"+{amount}")
        return f"Добавлено {amount} руб."
    
    def withdraw(self, amount):
        """Снять деньги"""
        if amount > self.balance:
            return "Ошибка: недостаточно средств!"
        self.balance -= amount
        self.transactions.append(f"-{amount}")
        return f"Снято {amount} руб."
    
    def get_balance(self):
        """Получить баланс"""
        return self.balance
    
    def get_info(self):
        """Полная информация"""
        print(f"=== Счёт {self.owner} ===")
        print(f"Баланс: {self.balance} руб.")
        print(f"История операций: {', '.join(self.transactions)}")
    
    def transfer(self, other_account, amount):
        """Перевод на другой счёт"""
        if amount > self.balance:
            return "Ошибка: недостаточно средств!"
        self.withdraw(amount)
        other_account.deposit(amount)
        return f"Переведено {amount} руб. на счёт {other_account.owner}"

# Тестирование
account1 = BankAccount("Иван", 1000)
account2 = BankAccount("Мария", 500)

account1.deposit(500)
account1.get_info()

print(account1.transfer(account2, 300))

account2.get_info()
```

**Требования:**

- Используй `__init__` для инициализации
- Создай методы для операций
- Сохраняй историю операций
- Добавь метод трансфера между счётами

---

## 🎯 Связь со сквозным проектом

**Менеджер задач с классом!**

```python
class TaskManager:
    def __init__(self):
        self.tasks = []
    
    def add_task(self, title, priority=1):
        """Добавить задачу"""
        task = Task(title, priority)
        self.tasks.append(task)
    
    def mark_done(self, task_id):
        """Отметить как выполненную"""
        if 0 <= task_id < len(self.tasks):
            self.tasks[task_id].mark_completed()
    
    def show_all(self):
        """Показать все задачи"""
        for i, task in enumerate(self.tasks):
            print(f"{i+1}. {task.get_status()}")

# Использование
manager = TaskManager()
manager.add_task("Купить продукты", 1)
manager.add_task("Написать отчёт", 2)
manager.show_all()
```

---

## 💡 Важный совет: Не усложняй!

**Хороший класс:**

```python
class Car:
    def __init__(self, brand, year):
        self.brand = brand
        self.year = year
    
    def get_age(self):
        return 2024 - self.year
```

**Слишком сложный класс:**

```python
class Car:
    def __init__(self, brand, year, color, type, engine, ...):
        # 10 параметров!
        # 50 методов!
        # Это слишком!
        pass
```

**Правило:** Класс должен делать **одно** — группировать связанные данные и методы.

---

## Резюме: Три главных вывода

✅ **Класс = чертёж для создания объектов**

✅ **`self` = текущий объект (себя)**

✅ **Методы = функции, которые живут в классе**

---

## Что дальше?

→ **Глава 3.3** (Наследование): Как один класс может быть как другой

→ **Глава 3.4** (Модули): Как делить код на файлы

---

## 🌟 ПОЗДРАВЛЯЕМ!

Ты прошёл **классы** — концепцию, которая кажется сложной, но на самом деле очень полезна! 🎉

Классы помогают:

- 📦 **Группировать** данные и методы
- 🎯 **Организовывать** код
- 🔧 **Переиспользовать** код

**Дальше становится ещё интереснее!** 🚀✨