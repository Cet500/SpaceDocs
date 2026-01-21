# 4.2 Форматы данных: JSON, XML, YAML, TOML и другие

## Введение: Зачем нужны разные форматы?

Представь ситуацию:
- Мобильное приложение отправляет данные на сервер
- Сервер должен их прочитать
- Сохранить в базе данных
- Отправить другому приложению
- Сохранить в конфиге

Каждый этап нужна **одинаковая структура**, чтобы все поняли друг друга!

**Главная идея форматов:** это договор между программами.

```
Приложение 1          Приложение 2
    |                     |
    └─ JSON (договор) ───>
       (я отправляю так,
        ты получаешь так)
```

---

## Сравнение основных форматов

| Формат | Строки | Вложенность | Скорость | Читаемость | Где используется |
|--------|--------|------------|----------|-----------|-----------------|
| **JSON** | ❌ | ✅✅✅ | ✅✅ | ✅✅✅ | API, веб, конфиги |
| **XML** | ❌ | ✅✅✅ | ⚠️ | ⚠️ | SOAP, RSS, конфиги |
| **YAML** | ✅ | ✅✅ | ⚠️ | ✅✅✅ | Конфиги, Docker, Kubernetes |
| **TOML** | ✅ | ✅ | ✅✅ | ✅✅ | Python конфиги, Cargo |
| **CSV** | ✅ | ❌ | ✅✅✅ | ✅✅ | Таблицы, Excel |
| **Протобуф** | ❌ | ✅✅✅ | ✅✅✅ | ❌ | gRPC, Google, скорость |
| **Бинарный** | ❌ | ✅✅ | ✅✅✅ | ❌ | Изображения, видео, БД |

---

## 1. JSON: Король форматов 👑

### Почему JSON король?

**1. Простота**
```python
# Python словарь = JSON
{"name": "Иван", "age": 25}  # Это и Python, и JSON!
```

**2. Универсальность**
```
Python → JSON → JavaScript → Ruby → Go → Rust
(все его поддерживают!)
```

**3. Человеко-читаемость**
```json
{
  "name": "Иван",
  "age": 25
}
```
vs XML (много скобок)

**4. Структурированность**
- Объекты `{}`
- Массивы `[]`
- Примитивы (строки, числа, boolean)

### Структура JSON

```json
{
  "string": "текст",
  "number": 42,
  "float": 3.14,
  "boolean": true,
  "null": null,
  "array": [1, 2, 3],
  "object": {
    "nested": "данные"
  }
}
```

### Реальные примеры JSON

#### Пример 1: API ответ (GitHub)
```json
{
  "id": 1,
  "name": "octocat",
  "login": "octocat",
  "avatar_url": "https://github.com/images/error/octocat_happy.gif",
  "followers": 20,
  "public_repos": 2,
  "company": "GitHub"
}
```

#### Пример 2: Конфиг приложения
```json
{
  "database": {
    "host": "localhost",
    "port": 5432,
    "name": "myapp_db",
    "credentials": {
      "username": "admin",
      "password": "secret123"
    }
  },
  "server": {
    "port": 8000,
    "debug": true,
    "timeout": 30
  }
}
```

#### Пример 3: Интернет-магазин
```json
{
  "products": [
    {
      "id": 1,
      "name": "Ноутбук",
      "price": 50000,
      "currency": "RUB",
      "stock": 5,
      "tags": ["электроника", "компьютеры"]
    },
    {
      "id": 2,
      "name": "Мышка",
      "price": 1000,
      "currency": "RUB",
      "stock": 50,
      "tags": ["электроника", "аксессуары"]
    }
  ]
}
```

### Работа с JSON в Python

```python
import json

# JSON строка → Python объект (ДЕСЕРИАЛИЗАЦИЯ)
json_string = '{"name": "Иван", "age": 25}'
data = json.loads(json_string)
print(data['name'])  # Иван
print(data['age'])   # 25
print(type(data))    # <class 'dict'>

# Python объект → JSON строка (СЕРИАЛИЗАЦИЯ)
user = {
    "name": "Мария",
    "age": 30,
    "skills": ["Python", "JavaScript"]
}
json_output = json.dumps(user)
print(json_output)  
# {"name": "Мария", "age": 30, "skills": ["Python", "JavaScript"]}

# Красивый вывод
pretty_json = json.dumps(user, indent=2)
print(pretty_json)
# {
#   "name": "Мария",
#   "age": 30,
#   "skills": [
#     "Python",
#     "JavaScript"
#   ]
# }
```

### Чтение/запись JSON файлов

```python
# Запись в файл
with open('user.json', 'w') as f:
    json.dump(user, f, indent=2)

# Чтение из файла
with open('user.json', 'r') as f:
    loaded_user = json.load(f)
    print(loaded_user)
```

### API запрос (реальный пример)

```python
import json
import requests

# Запрос к GitHub API
response = requests.get('https://api.github.com/users/octocat')

# Получаем JSON и преобразуем в Python объект
user_data = response.json()  # Автоматическое парсинг JSON!

print(f"Логин: {user_data['login']}")
print(f"Фолловеры: {user_data['followers']}")
print(f"Репозитории: {user_data['public_repos']}")
```

---

## 2. XML: Старший брат JSON 📜

### Структура XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
  <user>
    <name>Иван</name>
    <age>25</age>
    <email>ivan@example.com</email>
  </user>
  <user>
    <name>Мария</name>
    <age>30</age>
    <email>maria@example.com</email>
  </user>
</root>
```

### XML vs JSON (один и тот же объект)

**JSON (компактный):**
```json
{
  "users": [
    {"name": "Иван", "age": 25},
    {"name": "Мария", "age": 30}
  ]
}
```

**XML (многословный):**
```xml
<users>
  <user>
    <name>Иван</name>
    <age>25</age>
  </user>
  <user>
    <name>Мария</name>
    <age>30</age>
  </user>
</users>
```

### Где используется XML

1. **RSS ленты** (новости)
```xml
<rss>
  <channel>
    <item>
      <title>Новость 1</title>
      <description>Описание</description>
      <link>https://...</link>
    </item>
  </channel>
</rss>
```

2. **SOAP (старые API)**
```xml
<soap:Envelope>
  <soap:Body>
    <GetUser>
      <id>123</id>
    </GetUser>
  </soap:Body>
</soap:Envelope>
```

3. **Конфиги (Spring, Java)**
```xml
<configuration>
  <database>
    <host>localhost</host>
    <port>5432</port>
  </database>
</configuration>
```

### Работа с XML в Python

```python
import xml.etree.ElementTree as ET

# Парсинг XML
xml_string = '''<?xml version="1.0"?>
<users>
  <user>
    <name>Иван</name>
    <age>25</age>
  </user>
  <user>
    <name>Мария</name>
    <age>30</age>
  </user>
</users>'''

root = ET.fromstring(xml_string)

# Перебираем пользователей
for user in root.findall('user'):
    name = user.find('name').text
    age = user.find('age').text
    print(f"{name}: {age} лет")
    
# Вывод:
# Иван: 25 лет
# Мария: 30 лет

# Создание XML
new_root = ET.Element('users')
user_elem = ET.SubElement(new_root, 'user')
name_elem = ET.SubElement(user_elem, 'name')
name_elem.text = 'Петр'

# Сохранение в файл
tree = ET.ElementTree(new_root)
tree.write('output.xml')
```

### Почему JSON выиграл?

| Причина | Объяснение |
|---------|-----------|
| **Компактность** | JSON на 30-50% меньше XML |
| **Простота** | Меньше синтаксиса, проще парсить |
| **Скорость** | Быстрее парсить и сериализовать |
| **Веб 2.0** | AJAX использует JSON, не XML |
| **Читаемость** | Человек понимает JSON лучше |

---

## 3. YAML: Конфиги для людей 📝

### Структура YAML

```yaml
# Без кавычек и фигурных скобок!
database:
  host: localhost
  port: 5432
  name: myapp_db
  credentials:
    username: admin
    password: secret123

server:
  port: 8000
  debug: true
  timeout: 30

# Списки
tags:
  - python
  - backend
  - django
```

### YAML vs JSON (один и тот же)

**JSON:**
```json
{
  "database": {
    "host": "localhost",
    "port": 5432
  }
}
```

**YAML (проще для человека):**
```yaml
database:
  host: localhost
  port: 5432
```

### Docker Compose (типичный пример YAML)

```yaml
version: '3.8'
services:
  web:
    image: python:3.9
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    environment:
      - DEBUG=True
      - DATABASE_URL=postgresql://user:pass@db:5432/mydb
    command: python manage.py runserver 0.0.0.0:8000

  db:
    image: postgres:13
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### Kubernetes (конфиг на YAML)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
        ports:
        - containerPort: 8000
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
```

### Работа с YAML в Python

```python
import yaml

# Парсинг YAML
yaml_string = '''
database:
  host: localhost
  port: 5432
users:
  - name: Иван
    age: 25
  - name: Мария
    age: 30
'''

data = yaml.safe_load(yaml_string)
print(data['database']['host'])  # localhost
print(data['users'][0]['name'])  # Иван

# Сохранение в YAML
config = {
    'database': {'host': 'localhost', 'port': 5432},
    'debug': True,
    'workers': 4
}

with open('config.yaml', 'w') as f:
    yaml.dump(config, f, default_flow_style=False)

# Чтение из файла
with open('config.yaml', 'r') as f:
    loaded_config = yaml.safe_load(f)
```

### Особенности YAML

**Минусы:**
- Чувствителен к отступам (легко ошибиться)
- Медленнее, чем JSON
- Сложнее в парсинге

```yaml
# Ошибка: неправильные отступы!
database:
  host: localhost
 port: 5432  # ← ОШИБКА! Неправильный отступ
```

---

## 4. TOML: Конфиги с наиболее понятным синтаксисом 🎯

### Структура TOML

```toml
[database]
host = "localhost"
port = 5432
name = "myapp_db"

[database.credentials]
username = "admin"
password = "secret123"

[server]
port = 8000
debug = true
timeout = 30

# Список
tags = ["python", "backend", "django"]
```

### Pyproject.toml (Python проект)

```toml
[project]
name = "my-app"
version = "1.0.0"
description = "Моё приложение"
authors = [
    {name = "Иван", email = "ivan@example.com"}
]
dependencies = [
    "django>=4.0",
    "requests>=2.28.0",
    "psycopg2-binary>=2.9.0"
]

[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = "test_*.py"
addopts = "-v"

[tool.black]
line-length = 100
target-version = ['py39']

[tool.pylint.messages_control]
disable = ["C0111", "C0103"]
```

### Cargo.toml (Rust)

```toml
[package]
name = "my-app"
version = "0.1.0"
edition = "2021"

[dependencies]
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1", features = ["full"] }
reqwest = "0.11"

[dev-dependencies]
pytest = "1.0"
```

### Работа с TOML в Python

```python
import toml

# Парсинг TOML
toml_string = '''
[database]
host = "localhost"
port = 5432

[server]
debug = true
workers = 4
'''

config = toml.loads(toml_string)
print(config['database']['host'])  # localhost

# Чтение файла
with open('pyproject.toml', 'r') as f:
    project_config = toml.load(f)

# Запись
with open('config.toml', 'w') as f:
    toml.dump(config, f)
```

---

## 5. CSV: Табличные данные 📊

### Структура CSV

```csv
name,age,email,city
Иван,25,ivan@example.com,Москва
Мария,30,maria@example.com,СПб
Петр,28,peter@example.com,Казань
```

### Реальный пример: Экспорт данных

```python
import csv

# Запись в CSV
users = [
    {'name': 'Иван', 'age': 25, 'email': 'ivan@example.com'},
    {'name': 'Мария', 'age': 30, 'email': 'maria@example.com'},
]

with open('users.csv', 'w', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=['name', 'age', 'email'])
    writer.writeheader()
    writer.writerows(users)

# Чтение из CSV
with open('users.csv', 'r') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"{row['name']}: {row['age']} лет")
```

### CSV с Pandas (вычисления)

```python
import pandas as pd

# Чтение
df = pd.read_csv('users.csv')

# Анализ
print(df.mean())      # Средний возраст
print(df.groupby('city').size())  # Группировка по городу

# Запись
df.to_csv('users_processed.csv', index=False)
```

---

## 6. Протобуф (Protocol Buffers): Скорость и компактность ⚡

### Определение структуры (proto файл)

```protobuf
syntax = "proto3";

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
  int32 age = 4;
}

message UserList {
  repeated User users = 1;
}
```

### Генерация и использование

```bash
# Компиляция
protoc --python_out=. user.pb2.proto
```

```python
import user_pb2

# Создание
user = user_pb2.User()
user.id = 1
user.name = "Иван"
user.email = "ivan@example.com"
user.age = 25

# Сериализация (очень компактная)
binary_data = user.SerializeToString()
print(len(binary_data))  # ~30 байт вместо 100+ для JSON!

# Десериализация
loaded_user = user_pb2.User()
loaded_user.ParseFromString(binary_data)
print(loaded_user.name)  # Иван
```

### Когда использовать Протобуф?

✅ **Используй:**
- High-load системы (Google, Netflix)
- Микросервисы (gRPC)
- Мобильные приложения
- Когда нужна максимальная скорость

❌ **Не используй:**
- Маленькие проекты
- Когда нужна читаемость
- Прототипы

---

## 7. Сериализация vs Десериализация 🔄

### Определение

**Сериализация** = преобразование объекта в строку/байты
```python
объект → строка (можно сохранить/отправить)
```

**Десериализация** = обратное преобразование
```python
строка → объект (можно использовать в коде)
```

### Практический пример

```python
import json

# ============== СЕРИАЛИЗАЦИЯ ==============
user = {
    "name": "Иван",
    "age": 25,
    "skills": ["Python", "Django"]
}

# Python объект → JSON строка
json_string = json.dumps(user)
print(json_string)
# {"name": "Иван", "age": 25, "skills": ["Python", "Django"]}

# Сохранение в файл
with open('user.json', 'w') as f:
    f.write(json_string)

# ============== ДЕСЕРИАЛИЗАЦИЯ ==============
# Чтение из файла
with open('user.json', 'r') as f:
    loaded_json = f.read()

# JSON строка → Python объект
loaded_user = json.loads(loaded_json)
print(loaded_user['name'])  # Иван
print(type(loaded_user))    # <class 'dict'>

# Можно использовать!
print(f"Привет, {loaded_user['name']}!")
```

### Сериализация через стандартную библиотеку

```python
import pickle  # Встроенный модуль Python

user = {
    "name": "Иван",
    "age": 25,
}

# Сериализация в бинарный формат
binary_data = pickle.dumps(user)

# Десериализация
loaded_user = pickle.loads(binary_data)
print(loaded_user)  # {'name': 'Иван', 'age': 25}
```

### API запрос: реальная сериализация/десериализация

```python
import json
import requests

# ============ ОТПРАВКА (сериализация) ============
user_data = {
    "name": "Иван",
    "email": "ivan@example.com",
    "age": 25
}

# Python объект → JSON строка
response = requests.post(
    'https://api.example.com/users',
    data=json.dumps(user_data),  # Сериализуем!
    headers={'Content-Type': 'application/json'}
)

# ============ ПОЛУЧЕНИЕ (десериализация) ============
# Сервер отвечает JSON
response_data = response.json()  # Десериализуем!

print(response_data['id'])  # Новый ID пользователя
```

---

## 8. Где что применять? 🎯

### JSON ✅ ИСПОЛЬЗУЙ ВЕЗДЕ

**Идеально для:**
- ✅ API (REST)
- ✅ Веб запросы (AJAX)
- ✅ Облачные сервисы
- ✅ Микросервисы
- ✅ Конфиги (современные)
- ✅ Логирование
- ✅ Мобильные приложения

**Почему?**
- Все его поддерживают
- Быстро парсить
- Компактный
- Человек читает
- Стандарт де-факто

```json
{
  "status": "success",
  "data": {
    "id": 1,
    "name": "Иван"
  }
}
```

---

### YAML 🐳 ИСПОЛЬЗУЙ ДЛЯ КОНФИГОВ

**Идеально для:**
- ✅ Docker Compose
- ✅ Kubernetes
- ✅ CI/CD (GitHub Actions, GitLab CI)
- ✅ Конфиги приложений
- ✅ IaC (Infrastructure as Code)

**Почему?**
- Читается как текст
- Минимум синтаксиса
- Версионируется в Git
- Люди понимают быстро

```yaml
# Ясно даже без опыта!
services:
  web:
    image: python:3.9
    ports:
      - "8000:8000"
  db:
    image: postgres:13
```

---

### TOML 🦀 ИСПОЛЬЗУЙ ДЛЯ ПРОЕКТОВ

**Идеально для:**
- ✅ `pyproject.toml` (Python)
- ✅ `Cargo.toml` (Rust)
- ✅ Конфиги приложений
- ✅ Версии и зависимости

**Почему?**
- Явная структура
- Стандарт для языков
- Не проблема отступов (как YAML)
- Четкие типы данных

```toml
[project]
name = "my-app"
version = "1.0.0"

[tool.pytest]
testpaths = ["tests"]
```

---

### XML ❌ ИЗБЕГАЙ (в новых проектах)

**Используй только для:**
- ⚠️ SOAP (старые API)
- ⚠️ RSS ленты (нет выбора)
- ⚠️ Конфиги Java (legacy)
- ⚠️ Android (native XML)

**Почему избегать?**
- Слишком многословный
- Медленно парсить
- JSON компактнее на 30-50%
- Молодые разработчики не знают

```xml
<!-- Много кода для простого объекта! -->
<user>
  <name>Иван</name>
  <age>25</age>
</user>
```

---

### CSV 📊 ИСПОЛЬЗУЙ ДЛЯ ТАБЛИЦ

**Идеально для:**
- ✅ Экспорт из БД
- ✅ Excel/Sheets интеграция
- ✅ Отчеты
- ✅ Batch обработка
- ✅ Pandas анализ

**Почему?**
- Все офисные программы понимают
- Легко открыть в Excel
- Компактный для больших таблиц
- Стандарт обмена данными

```csv
name,age,city
Иван,25,Москва
Мария,30,СПб
```

---

### Протобуф ⚡ ИСПОЛЬЗУЙ ДЛЯ СКОРОСТИ

**Идеально для:**
- ✅ gRPC (микросервисы)
- ✅ High-load системы
- ✅ Мобильные приложения
- ✅ Когда объём критичен
- ✅ Google, Netflix, Facebook

**Почему?**
- Компактнее JSON на 5-10x
- Быстрее парсить
- Строгая типизация
- Версионируется

```protobuf
message User {
  int32 id = 1;
  string name = 2;
}
```

---

## 9. Реальные примеры использования

### Пример 1: Приложение для заказов

**Фронтенд отправляет заказ:**
```python
# Сериализация
import json

order = {
    "user_id": 123,
    "items": [
        {"product_id": 1, "quantity": 2, "price": 1000},
        {"product_id": 2, "quantity": 1, "price": 5000}
    ],
    "total": 7000,
    "delivery": {
        "address": "ул. Пушкина, 1",
        "city": "Москва",
        "phone": "+7-999-123-45-67"
    }
}

# Отправляем в виде JSON
json_order = json.dumps(order)
requests.post('https://api.shop.com/orders', data=json_order)
```

**Бэкенд получает и обрабатывает:**
```python
from flask import Flask, request
import json

app = Flask(__name__)

@app.route('/orders', methods=['POST'])
def create_order():
    # Десериализация
    order_data = request.json  # Автоматическое парсинг JSON!
    
    # Валидация
    if order_data['total'] < 0:
        return {"error": "Invalid total"}, 400
    
    # Сохранение в БД
    order = Order.create(
        user_id=order_data['user_id'],
        items=order_data['items'],
        total=order_data['total'],
        delivery_address=order_data['delivery']['address']
    )
    
    # Отправляем ответ
    return {
        "id": order.id,
        "status": "created",
        "total": order.total
    }, 201
```

---

### Пример 2: Конфиг приложения

**config.yaml (человеко-читаемо):**
```yaml
# Параметры БД
database:
  host: localhost
  port: 5432
  name: myapp
  pool_size: 10

# Параметры сервера
server:
  host: 0.0.0.0
  port: 8000
  workers: 4
  debug: true

# Параметры логирования
logging:
  level: INFO
  file: logs/app.log

# Email уведомления
email:
  smtp_host: smtp.gmail.com
  smtp_port: 587
  from_email: noreply@myapp.com
```

**Загрузка в приложении:**
```python
import yaml

# Загружаем конфиг
with open('config.yaml', 'r') as f:
    config = yaml.safe_load(f)

# Используем
DATABASE_URL = f"postgresql://{config['database']['host']}:{config['database']['port']}/{config['database']['name']}"

DEBUG = config['server']['debug']
WORKERS = config['server']['workers']

# Логирование
logging.basicConfig(
    level=config['logging']['level'],
    filename=config['logging']['file']
)
```

---

### Пример 3: Docker Compose

```yaml
# docker-compose.yml - описываем всю архитектуру!
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    environment:
      - DEBUG=True
      - DATABASE_URL=postgresql://postgres:postgres@db:5432/myapp
    depends_on:
      - db
    volumes:
      - .:/app
    command: python manage.py runserver 0.0.0.0:8000

  db:
    image: postgres:13
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DB=myapp
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7
    ports:
      - "6379:6379"

volumes:
  postgres_data:
```

**Один файл = весь стек приложения!**

```bash
# Запускаем всё
docker-compose up

# Результат: Web + PostgreSQL + Redis работают вместе!
```

---

### Пример 4: GitHub Actions (CI/CD)

```yaml
# .github/workflows/tests.yml - автоматизация тестирования
name: Tests

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        python-version: ['3.9', '3.10', '3.11']
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v4
      with:
        python-version: ${{ matrix.python-version }}
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    
    - name: Run tests
      run: |
        pytest tests/ -v
    
    - name: Coverage
      run: |
        pip install coverage
        coverage run -m pytest
        coverage report
```

---

### Пример 5: pyproject.toml (полный конфиг)

```toml
# pyproject.toml - современный способ!
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "my-django-app"
version = "1.0.0"
description = "Приложение для управления проектами"
authors = [
    {name = "Иван Петров", email = "ivan@example.com"}
]
requires-python = ">=3.9"
dependencies = [
    "django>=4.0,<5.0",
    "djangorestframework>=3.13.0",
    "psycopg2-binary>=2.9.0",
    "celery>=5.2.0",
    "redis>=4.0.0",
    "requests>=2.28.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0.0",
    "pytest-django>=4.5.0",
    "black>=22.0.0",
    "flake8>=4.0.0",
    "mypy>=0.950",
]

[tool.pytest.ini_options]
DJANGO_SETTINGS_MODULE = "config.settings"
testpaths = ["tests"]
python_files = "test_*.py"
addopts = "-v --cov=myapp"

[tool.black]
line-length = 100
target-version = ['py39', 'py310']
exclude = '''
/(
    \.git
  | \.venv
  | migrations
)/
'''

[tool.mypy]
python_version = "3.9"
check_untyped_defs = true
strict = true

[tool.isort]
profile = "black"
line_length = 100
```

---

## 10. Производительность и размер

### Сравнение (один и тот же объект)

```
Объект: список из 1000 пользователей

JSON:      200 KB
XML:       500 KB  (2.5x больше!)
YAML:      180 KB  (меньше JSON)
Протобуф:  50 KB   (4x меньше JSON!)
```

### Скорость парсинга

```
JSON:      ✅ быстро (встроенная оптимизация)
XML:       ⚠️ медленнее (нужно парсить теги)
YAML:      ⚠️ медленнее (парсинг отступов)
Протобуф:  ✅✅ очень быстро (бинарный)
```

---

## 11. Практическое задание

### Задание: Конвертер форматов

Напиши программу, которая:

```python
# 1. Читает JSON
# 2. Конвертирует в другие форматы
# 3. Показывает размер каждого

import json
import yaml

# Исходные данные (JSON)
json_data = '''
{
  "users": [
    {"id": 1, "name": "Иван", "email": "ivan@mail.com"},
    {"id": 2, "name": "Мария", "email": "maria@mail.com"},
    {"id": 3, "name": "Петр", "email": "peter@mail.com"}
  ]
}
'''

# 1. Парсим JSON
data = json.loads(json_data)

# 2. Сериализуем в разные форматы
json_output = json.dumps(data, indent=2)
yaml_output = yaml.dump(data, default_flow_style=False)

# 3. Сравниваем размеры
print(f"JSON размер:  {len(json_output)} байт")
print(f"YAML размер:  {len(yaml_output)} байт")
print(f"Компактный JSON: {len(json.dumps(data))} байт")

# 4. Выводим
print("\n=== JSON ===")
print(json_output)
print("\n=== YAML ===")
print(yaml_output)
```

**Ожидаемый вывод:**
```
JSON размер:  200 байт
YAML размер:  165 байт
Компактный JSON: 140 байт

=== JSON ===
{
  "users": [
    {
      "id": 1,
      "name": "Иван",
      "email": "ivan@mail.com"
    },
    ...
  ]
}

=== YAML ===
users:
- id: 1
  name: Иван
  email: ivan@mail.com
- id: 2
  name: Мария
  email: maria@mail.com
...
```

---

## Резюме: Чит-лист форматов

| Формат | Когда использовать | Когда НЕ использовать |
|--------|-------------------|----------------------|
| **JSON** | 99% случаев (API, веб, конфиги) | Очень большие объёмы (>1GB) |
| **YAML** | Конфиги, Docker, Kubernetes | Когда нужна максимальная скорость |
| **TOML** | Python конфиги, зависимости | Сложные структуры |
| **XML** | Только если нет выбора (SOAP, RSS) | Новые проекты (используй JSON!) |
| **CSV** | Таблицы, Excel, БД экспорт | Сложные структуры |
| **Протобуф** | gRPC, высокая нагрузка, мобильное | Прототипы, читаемость важна |

### Главное правило:

```
✅ JSON = значение по умолчанию для всего
⬇️
Если JSON не подходит → ищи альтернативу
⬇️
Если специфический формат нужен → выбирай из таблицы выше
```

---

## Что дальше?

✅ Ты знаешь основные форматы
✅ Ты можешь сериализовать и десериализовать
✅ Ты знаешь когда что использовать

**Следующий шаг:** Работа с файлами на диске!

В главе 4.3 мы научимся:
- Читать/писать файлы
- Работать с путями
- Обработка ошибок
- Контекстные менеджеры
- Работа с большими файлами

**Готов?** 🚀