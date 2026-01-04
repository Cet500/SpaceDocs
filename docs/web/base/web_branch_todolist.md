# ✅ Проект: Список дел (To-Do List)

## Идея проекта

Ты создашь классический список дел — приложение, где можно добавлять задачи, отмечать их как выполненные и удалять.

**Что тренируется:**

- Работа с HTML формами
- Манипуляция элементами страницы (DOM)
- Функции и события
- Локальное хранилище (LocalStorage, опционально)
- Условия и циклы

**Уровень сложности:** Средний (не нужны продвинутые знания)

---

## Модуль 1: Основная структура

### Задание 1.1: Создаём HTML структуру

**Что мы делаем:**
Создаём форму для ввода новых задач и список для их отображения.

**HTML структура:**

```html
<html>
  <head>
    <title>Мой список дел</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <div class="container">
      <h1>📋 Мой список дел</h1>
      
      <!-- Форма для добавления задачи -->
      <div class="input-group">
        <input 
          type="text" 
          id="taskInput" 
          placeholder="Введи новую задачу..."
        >
        <button onclick="addTask()">Добавить</button>
      </div>

      <!-- Статистика -->
      <div class="stats">
        <p>Всего: <span id="totalTasks">0</span></p>
        <p>Выполнено: <span id="completedTasks">0</span></p>
      </div>

      <!-- Список задач -->
      <ul id="taskList" class="task-list">
        <!-- Задачи будут добавлены сюда -->
      </ul>
    </div>

    <script src="script.js"></script>
  </body>
</html>
```

**Что здесь:**

- `input` — поле для ввода новой задачи.
- `button` — кнопка для добавления задачи.
- `taskList` — контейнер для всех задач (будет заполнен JavaScript'ом).
- `stats` — показывает статистику.

**Что попробовать:**

1. Открой HTML в браузере. Видишь форму?
2. Попробуй что-нибудь напечатать в поле ввода (пока ничего не будет происходить).

---

## Модуль 2: Стили (CSS)

### Задание 2.1: Красивый дизайн списка

**CSS (`style.css`):**

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  max-width: 500px;
  width: 90%;
  padding: 30px;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
}

/* Форма */
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

#taskInput {
  flex: 1;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 16px;
  transition: border-color 0.3s;
}

#taskInput:focus {
  outline: none;
  border-color: #667eea;
}

button {
  padding: 12px 25px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  font-size: 16px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #5568d3;
}

/* Статистика */
.stats {
  display: flex;
  justify-content: space-around;
  background-color: #f5f5f5;
  padding: 15px;
  border-radius: 6px;
  margin-bottom: 20px;
  font-size: 14px;
  color: #666;
}

.stats span {
  font-weight: bold;
  color: #333;
}

/* Список задач */
.task-list {
  list-style: none;
}

.task-item {
  display: flex;
  align-items: center;
  padding: 15px;
  background-color: #f9f9f9;
  border-radius: 6px;
  margin-bottom: 10px;
  transition: all 0.3s;
}

.task-item:hover {
  background-color: #f0f0f0;
  transform: translateX(5px);
}

/* Чекбокс */
.task-item input[type="checkbox"] {
  width: 20px;
  height: 20px;
  cursor: pointer;
  margin-right: 12px;
}

.task-item input[type="checkbox"]:checked + .task-text {
  text-decoration: line-through;
  color: #999;
}

.task-text {
  flex: 1;
  color: #333;
  font-size: 16px;
}

/* Кнопка удаления */
.delete-btn {
  background-color: #ff6b6b;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

.delete-btn:hover {
  background-color: #ff5252;
}

/* Пустой список */
.empty-message {
  text-align: center;
  color: #999;
  padding: 30px;
  font-size: 16px;
}
```

**Что попробовать:**

1. Измени цвета.
2. Измени шрифт.
3. Добавь собственные стили.

---

## Модуль 3: JavaScript функционал

### Задание 3.1: Добавление задач

**JavaScript (`script.js`):**

```javascript
// Массив для хранения задач
let tasks = [];

// Добавить новую задачу
function addTask() {
  let input = document.getElementById("taskInput");
  let taskText = input.value.trim();  // Получить текст и убрать пробелы

  // Проверка: пусто ли поле?
  if (taskText === "") {
    alert("Введи задачу!");
    return;
  }

  // Создать объект задачи
  let task = {
    id: Date.now(),        // Уникальный ID (текущее время)
    text: taskText,
    completed: false
  };

  // Добавить в массив
  tasks.push(task);

  // Очистить поле ввода
  input.value = "";

  // Обновить список на странице
  renderTasks();

  // Сфокусировать на поле ввода
  input.focus();
}

// Отобразить все задачи
function renderTasks() {
  let taskList = document.getElementById("taskList");
  taskList.innerHTML = "";  // Очистить старый список

  // Если нет задач, показать сообщение
  if (tasks.length === 0) {
    taskList.innerHTML = '<div class="empty-message">Нет задач. Добавь одну!</div>';
    updateStats();
    return;
  }

  // Для каждой задачи создать элемент
  for (let i = 0; i < tasks.length; i++) {
    let task = tasks[i];

    // Создать элемент задачи
    let li = document.createElement("li");
    li.className = "task-item";

    // Чекбокс
    let checkbox = document.createElement("input");
    checkbox.type = "checkbox";
    checkbox.checked = task.completed;
    checkbox.onchange = function() {
      toggleTask(task.id);
    };

    // Текст задачи
    let span = document.createElement("span");
    span.className = "task-text";
    span.textContent = task.text;

    // Кнопка удаления
    let deleteBtn = document.createElement("button");
    deleteBtn.className = "delete-btn";
    deleteBtn.textContent = "Удалить";
    deleteBtn.onclick = function() {
      deleteTask(task.id);
    };

    // Собрать элемент
    li.appendChild(checkbox);
    li.appendChild(span);
    li.appendChild(deleteBtn);

    // Добавить в список
    taskList.appendChild(li);
  }

  // Обновить статистику
  updateStats();
}

// Отметить задачу как выполненную
function toggleTask(id) {
  // Найти задачу по ID
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === id) {
      tasks[i].completed = !tasks[i].completed;
      break;
    }
  }

  // Обновить список
  renderTasks();
}

// Удалить задачу
function deleteTask(id) {
  // Найти и удалить задачу
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].id === id) {
      tasks.splice(i, 1);  // Удалить элемент из массива
      break;
    }
  }

  // Обновить список
  renderTasks();
}

// Обновить статистику
function updateStats() {
  let totalCount = tasks.length;
  let completedCount = 0;

  // Считать выполненные задачи
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].completed) {
      completedCount++;
    }
  }

  // Обновить на странице
  document.getElementById("totalTasks").textContent = totalCount;
  document.getElementById("completedTasks").textContent = completedCount;
}

// Позволить добавлять задачу нажатием Enter
document.addEventListener("DOMContentLoaded", function() {
  let input = document.getElementById("taskInput");
  input.addEventListener("keypress", function(event) {
    if (event.key === "Enter") {
      addTask();
    }
  });
});
```

**Что происходит:**

1. `addTask()` — добавляет новую задачу в массив.
2. `renderTasks()` — отображает все задачи на странице.
3. `toggleTask()` — отмечает задачу как выполненную.
4. `deleteTask()` — удаляет задачу.
5. `updateStats()` — обновляет счётчик.

**Что попробовать:**

1. Добавь несколько задач.
2. Отметь некоторые как выполненные.
3. Удали задачу.
4. Посмотри, как меняется статистика.

---

## Модуль 4: Улучшения и бонусы

### Задание 4.1: Локальное хранилище (LocalStorage)

**Что мы делаем:**
Сохраняем задачи так, чтобы они остались после перезагрузки страницы.

**Добавь в `script.js`:**

```javascript
// Сохранить задачи в браузер
function saveTasks() {
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

// Загрузить задачи из браузера
function loadTasks() {
  let saved = localStorage.getItem("tasks");
  if (saved) {
    tasks = JSON.parse(saved);
    renderTasks();
  }
}

// Загрузить задачи при открытии страницы
document.addEventListener("DOMContentLoaded", function() {
  loadTasks();  // Загрузить сохранённые задачи

  // ... остальной код ...
});

// Сохранять после каждого действия
function addTask() {
  // ... остальной код ...
  saveTasks();  // Добавить эту строку
}

function toggleTask(id) {
  // ... остальной код ...
  saveTasks();  // Добавить эту строку
}

function deleteTask(id) {
  // ... остальной код ...
  saveTasks();  // Добавить эту строку
}
```

**Что попробовать:**

1. Добавь задачу.
2. Перезагрузи страницу (F5).
3. Задача должна быть на месте!

---

### Задание 4.2: Фильтрация задач

**Что мы делаем:**
Добавляем кнопки для фильтрации (все, выполненные, невыполненные).

**Добавь в HTML:**

```html
<!-- Кнопки фильтрации -->
<div class="filter-buttons">
  <button onclick="showAll()">Все</button>
  <button onclick="showActive()">Активные</button>
  <button onclick="showCompleted()">Выполненные</button>
</div>
```

**Добавь в CSS:**

```css
.filter-buttons {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  justify-content: center;
}

.filter-buttons button {
  flex: 1;
  padding: 8px 12px;
  background-color: #f0f0f0;
  color: #333;
  border: 2px solid #ddd;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  transition: all 0.3s;
}

.filter-buttons button:hover,
.filter-buttons button.active {
  background-color: #667eea;
  color: white;
  border-color: #667eea;
}
```

**Добавь в JavaScript:**

```javascript
let filter = "all";  // Текущий фильтр

function showAll() {
  filter = "all";
  renderTasks();
}

function showActive() {
  filter = "active";
  renderTasks();
}

function showCompleted() {
  filter = "completed";
  renderTasks();
}

// Модифицируй renderTasks для фильтрации
function renderTasks() {
  let taskList = document.getElementById("taskList");
  taskList.innerHTML = "";

  // Отфильтровать задачи
  let filteredTasks = [];
  for (let i = 0; i < tasks.length; i++) {
    if (filter === "all") {
      filteredTasks.push(tasks[i]);
    } else if (filter === "active" && !tasks[i].completed) {
      filteredTasks.push(tasks[i]);
    } else if (filter === "completed" && tasks[i].completed) {
      filteredTasks.push(tasks[i]);
    }
  }

  // Остальной код renderTasks...
  // но используй filteredTasks вместо tasks
}
```

**Что попробовать:**

1. Добавь несколько задач.
2. Отметь некоторые как выполненные.
3. Фильтруй по состоянию.

---

### Задание 4.3: Очистить все

**Что мы делаем:**
Добавляем кнопку для удаления всех задач.

**Добавь в HTML:**

```html
<button onclick="clearAll()" class="clear-btn">Очистить всё</button>
```

**Добавь в CSS:**

```css
.clear-btn {
  background-color: #ff6b6b;
  width: 100%;
  margin-top: 20px;
}

.clear-btn:hover {
  background-color: #ff5252;
}
```

**Добавь в JavaScript:**

```javascript
function clearAll() {
  if (confirm("Уверен? Все задачи будут удалены!")) {
    tasks = [];
    renderTasks();
    saveTasks();
  }
}
```

---

## Итоговая проверка

**Функционал, который должен работать:**

- [ ] Добавление новых задач (через кнопку и Enter)
- [ ] Отметить задачу как выполненную (чекбокс)
- [ ] Удалить отдельную задачу
- [ ] Статистика (всего / выполнено)
- [ ] Сохранение в браузер (LocalStorage)
- [ ] Фильтрация (все / активные / выполненные)
- [ ] Очистка всех задач
- [ ] Красивый дизайн

**Бонусные фишки:**

- Добавить приоритет (высокий, средний, низкий)
- Добавить дату создания
- Сортировка по дате
- Редактирование задач
- Темный режим

---

Отлично! Ты создал полноценное веб-приложение! 🚀
