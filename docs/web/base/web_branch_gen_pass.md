# 🔐 Проект: Генератор паролей

## Идея проекта

Ты создашь инструмент, который генерирует случайные, надёжные пароли с разными настройками: длина, использование букв,
цифр, специальных символов.

**Что тренируется:**

- Работа с инпутами и слайдерами
- Случайные числа (Math.random)
- Массивы и циклы
- Функции
- Работа со строками
- Копирование в буфер обмена (bonus)

**Уровень сложности:** Средний

---

## Модуль 1: Основная структура

### Задание 1.1: Создаём интерфейс

**HTML (`index.html`):**

```html
<html>
  <head>
    <title>Генератор паролей</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <div class="container">
      <h1>🔐 Генератор паролей</h1>

      <!-- Отображение пароля -->
      <div class="password-display">
        <input 
          type="text" 
          id="passwordOutput" 
          readonly 
          placeholder="Пароль появится здесь"
        >
        <button onclick="copyPassword()" class="copy-btn">Копировать</button>
      </div>

      <!-- Слайдер для длины -->
      <div class="option">
        <label>Длина пароля: <span id="lengthValue">12</span></label>
        <input 
          type="range" 
          id="lengthSlider" 
          min="4" 
          max="32" 
          value="12"
          onchange="updateLengthValue()"
        >
      </div>

      <!-- Чекбоксы для опций -->
      <div class="options-group">
        <label>
          <input type="checkbox" id="uppercase" checked>
          Заглавные буквы (A-Z)
        </label>
        <label>
          <input type="checkbox" id="lowercase" checked>
          Строчные буквы (a-z)
        </label>
        <label>
          <input type="checkbox" id="numbers" checked>
          Цифры (0-9)
        </label>
        <label>
          <input type="checkbox" id="symbols" checked>
          Специальные символы (!@#$)
        </label>
      </div>

      <!-- Кнопка генерации -->
      <button onclick="generatePassword()" class="generate-btn">
        Сгенерировать пароль
      </button>

      <!-- Показатель крепости -->
      <div class="strength-indicator">
        <p>Крепость пароля:</p>
        <div class="strength-bar">
          <div id="strengthFill" class="strength-fill"></div>
        </div>
        <p id="strengthText" class="strength-text">—</p>
      </div>

      <!-- История -->
      <div class="history">
        <h3>История пароля:</h3>
        <button onclick="clearHistory()" class="clear-btn">Очистить</button>
        <ul id="historyList" class="history-list">
          <li class="empty-message">История пуста</li>
        </ul>
      </div>
    </div>

    <script src="script.js"></script>
  </body>
</html>
```

**Что здесь:**

- `passwordOutput` — поле с сгенерированным паролем.
- `lengthSlider` — выбор длины пароля.
- Чекбоксы для выбора символов.
- `passwordOutput` — отображение пароля.
- `historyList` — история сгенерированных паролей.

---

## Модуль 2: Стили (CSS)

### Задание 2.1: Красивый дизайн

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
  padding: 20px;
}

.container {
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  max-width: 500px;
  width: 100%;
  padding: 30px;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  font-size: 28px;
}

/* Отображение пароля */
.password-display {
  display: flex;
  gap: 10px;
  margin-bottom: 25px;
}

#passwordOutput {
  flex: 1;
  padding: 15px;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 18px;
  font-family: 'Courier New', monospace;
  letter-spacing: 2px;
  transition: border-color 0.3s;
}

#passwordOutput:focus {
  outline: none;
  border-color: #667eea;
}

.copy-btn {
  padding: 15px 20px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s;
  white-space: nowrap;
}

.copy-btn:hover {
  background-color: #5568d3;
}

.copy-btn:active {
  transform: scale(0.98);
}

/* Опции */
.option {
  margin-bottom: 20px;
}

.option label {
  display: block;
  color: #333;
  font-weight: bold;
  margin-bottom: 8px;
}

.option input[type="range"] {
  width: 100%;
  height: 6px;
  border-radius: 3px;
  background: linear-gradient(to right, #ddd 0%, #667eea 100%);
  outline: none;
  -webkit-appearance: none;
}

.option input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background-color: #667eea;
  cursor: pointer;
  transition: background-color 0.3s;
}

.option input[type="range"]::-webkit-slider-thumb:hover {
  background-color: #5568d3;
}

/* Чекбоксы */
.options-group {
  background-color: #f9f9f9;
  padding: 15px;
  border-radius: 6px;
  margin-bottom: 20px;
}

.options-group label {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  color: #333;
  cursor: pointer;
  transition: color 0.3s;
}

.options-group label:last-child {
  margin-bottom: 0;
}

.options-group label:hover {
  color: #667eea;
}

.options-group input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
  margin-right: 10px;
  accent-color: #667eea;
}

/* Кнопка генерации */
.generate-btn {
  width: 100%;
  padding: 15px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-bottom: 20px;
}

.generate-btn:hover {
  background-color: #5568d3;
}

.generate-btn:active {
  transform: scale(0.98);
}

/* Показатель крепости */
.strength-indicator {
  background-color: #f9f9f9;
  padding: 15px;
  border-radius: 6px;
  margin-bottom: 20px;
}

.strength-indicator p {
  color: #666;
  font-size: 14px;
  margin-bottom: 8px;
}

.strength-bar {
  height: 8px;
  background-color: #ddd;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 8px;
}

.strength-fill {
  height: 100%;
  background-color: #ff6b6b;
  width: 0%;
  transition: width 0.3s, background-color 0.3s;
}

.strength-text {
  font-size: 12px;
  color: #666;
  font-weight: bold;
}

/* История */
.history {
  background-color: #f9f9f9;
  padding: 15px;
  border-radius: 6px;
}

.history h3 {
  color: #333;
  font-size: 16px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.clear-btn {
  padding: 6px 12px;
  background-color: #ff6b6b;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  transition: background-color 0.3s;
}

.clear-btn:hover {
  background-color: #ff5252;
}

.history-list {
  list-style: none;
  max-height: 150px;
  overflow-y: auto;
}

.history-list li {
  padding: 8px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-bottom: 6px;
  font-family: 'Courier New', monospace;
  font-size: 13px;
  color: #333;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.history-list li:last-child {
  margin-bottom: 0;
}

.empty-message {
  text-align: center;
  color: #999;
  padding: 20px;
}

.copy-history-btn {
  padding: 4px 8px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  font-size: 11px;
  transition: background-color 0.3s;
}

.copy-history-btn:hover {
  background-color: #5568d3;
}
```

---

## Модуль 3: JavaScript функционал

### Задание 3.1: Генерация паролей

**JavaScript (`script.js`):**

```javascript
// Символы для генерации
const UPPERCASE = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const LOWERCASE = "abcdefghijklmnopqrstuvwxyz";
const NUMBERS = "0123456789";
const SYMBOLS = "!@#$%^&*()_+-=[]{}|;:,.<>?";

// История паролей
let history = [];

// Обновить значение длины на экране
function updateLengthValue() {
  let slider = document.getElementById("lengthSlider");
  document.getElementById("lengthValue").textContent = slider.value;
}

// Получить случайный символ из строки
function getRandomCharacter(characters) {
  let randomIndex = Math.floor(Math.random() * characters.length);
  return characters[randomIndex];
}

// Сгенерировать пароль
function generatePassword() {
  // Получить параметры
  let length = parseInt(document.getElementById("lengthSlider").value);
  let useUppercase = document.getElementById("uppercase").checked;
  let useLowercase = document.getElementById("lowercase").checked;
  let useNumbers = document.getElementById("numbers").checked;
  let useSymbols = document.getElementById("symbols").checked;

  // Проверка: выбран хотя бы один тип символов?
  if (!useUppercase && !useLowercase && !useNumbers && !useSymbols) {
    alert("Выбери хотя бы один тип символов!");
    return;
  }

  // Собрать все допустимые символы
  let allCharacters = "";
  if (useUppercase) allCharacters += UPPERCASE;
  if (useLowercase) allCharacters += LOWERCASE;
  if (useNumbers) allCharacters += NUMBERS;
  if (useSymbols) allCharacters += SYMBOLS;

  // Сгенерировать пароль
  let password = "";
  for (let i = 0; i < length; i++) {
    password += getRandomCharacter(allCharacters);
  }

  // Вывести пароль
  document.getElementById("passwordOutput").value = password;

  // Обновить показатель крепости
  updatePasswordStrength(password);

  // Добавить в историю
  addToHistory(password);
}

// Оценить крепость пароля
function updatePasswordStrength(password) {
  let strength = 0;
  let strengthText = "";
  let strengthFill = document.getElementById("strengthFill");

  // Проверки
  if (password.length >= 8) strength += 20;
  if (password.length >= 12) strength += 10;
  if (password.length >= 16) strength += 10;

  if (/[A-Z]/.test(password)) strength += 15;  // Заглавные буквы
  if (/[a-z]/.test(password)) strength += 15;  // Строчные буквы
  if (/[0-9]/.test(password)) strength += 15;  // Цифры
  if (/[!@#$%^&*()_+\-=\[\]{}|;:,.<>?]/.test(password)) strength += 15;  // Спецсимволы

  // Определить текст и цвет
  if (strength < 30) {
    strengthText = "Слабый";
    strengthFill.style.backgroundColor = "#ff6b6b";
  } else if (strength < 60) {
    strengthText = "Средний";
    strengthFill.style.backgroundColor = "#ffd93d";
  } else if (strength < 80) {
    strengthText = "Хороший";
    strengthFill.style.backgroundColor = "#6bcf7f";
  } else {
    strengthText = "Сильный";
    strengthFill.style.backgroundColor = "#4ecdc4";
  }

  // Обновить визуализацию
  strengthFill.style.width = strength + "%";
  document.getElementById("strengthText").textContent = strengthText;
}

// Копировать пароль в буфер обмена
function copyPassword() {
  let passwordField = document.getElementById("passwordOutput");
  
  if (passwordField.value === "") {
    alert("Сначала сгенерируй пароль!");
    return;
  }

  // Выбрать текст
  passwordField.select();

  // Копировать
  try {
    document.execCommand("copy");
    alert("Пароль скопирован в буфер обмена!");
  } catch (err) {
    alert("Ошибка при копировании");
  }
}

// Добавить пароль в историю
function addToHistory(password) {
  history.unshift(password);  // Добавить в начало

  // Ограничить историю до 10 паролей
  if (history.length > 10) {
    history.pop();
  }

  updateHistoryDisplay();
}

// Обновить отображение истории
function updateHistoryDisplay() {
  let historyList = document.getElementById("historyList");

  if (history.length === 0) {
    historyList.innerHTML = '<li class="empty-message">История пуста</li>';
    return;
  }

  historyList.innerHTML = "";

  for (let i = 0; i < history.length; i++) {
    let li = document.createElement("li");
    li.innerHTML = `
      <span>${history[i]}</span>
      <button class="copy-history-btn" onclick="copyHistoryPassword('${history[i]}')">
        Копировать
      </button>
    `;
    historyList.appendChild(li);
  }
}

// Копировать пароль из истории
function copyHistoryPassword(password) {
  // Поместить в поле и скопировать
  document.getElementById("passwordOutput").value = password;
  copyPassword();
}

// Очистить историю
function clearHistory() {
  if (confirm("Очистить историю паролей?")) {
    history = [];
    updateHistoryDisplay();
  }
}

// Генерировать пароль при загрузке страницы
document.addEventListener("DOMContentLoaded", function() {
  generatePassword();
});
```

**Что происходит:**

1. `generatePassword()` — создаёт случайный пароль из выбранных символов.
2. `updatePasswordStrength()` — оценивает крепость и показывает на шкале.
3. `copyPassword()` — копирует пароль в буфер обмена.
4. `addToHistory()` — сохраняет пароль в историю.
5. `clearHistory()` — удаляет всю историю.

**Что попробовать:**

1. Сгенерируй несколько паролей.
2. Измени длину и опции.
3. Копируй пароли.
4. Посмотри историю.

---

## Модуль 4: Улучшения

### Задание 4.1: Сохранение в LocalStorage

**Добавь в `script.js`:**

```javascript
// Сохранить историю
function saveHistory() {
  localStorage.setItem("passwordHistory", JSON.stringify(history));
}

// Загрузить историю
function loadHistory() {
  let saved = localStorage.getItem("passwordHistory");
  if (saved) {
    history = JSON.parse(saved);
    updateHistoryDisplay();
  }
}

// Загрузить историю при открытии страницы
document.addEventListener("DOMContentLoaded", function() {
  loadHistory();
  generatePassword();
});

// Сохранять после каждого добавления
function addToHistory(password) {
  history.unshift(password);
  if (history.length > 10) {
    history.pop();
  }
  updateHistoryDisplay();
  saveHistory();  // Добавить эту строку
}

// Сохранять при очистке
function clearHistory() {
  if (confirm("Очистить историю паролей?")) {
    history = [];
    updateHistoryDisplay();
    saveHistory();  // Добавить эту строку
  }
}
```

---

### Задание 4.2: Экспорт паролей

**Добавь в HTML:**

```html
<button onclick="exportPasswords()" class="export-btn">📥 Экспортировать</button>
```

**Добавь в CSS:**

```css
.export-btn {
  padding: 8px 12px;
  background-color: #667eea;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  transition: background-color 0.3s;
  margin-top: 10px;
}

.export-btn:hover {
  background-color: #5568d3;
}
```

**Добавь в JavaScript:**

```javascript
function exportPasswords() {
  if (history.length === 0) {
    alert("История пуста!");
    return;
  }

  let text = "История паролей:\n\n";
  for (let i = 0; i < history.length; i++) {
    text += (i + 1) + ". " + history[i] + "\n";
  }

  // Создать файл и скачать
  let element = document.createElement("a");
  element.setAttribute("href", "data:text/plain;charset=utf-8," + encodeURIComponent(text));
  element.setAttribute("download", "passwords.txt");
  element.style.display = "none";
  document.body.appendChild(element);
  element.click();
  document.body.removeChild(element);
}
```

---

## Итоговая проверка

**Функционал, который должен работать:**

- [ ] Генерация случайных паролей
- [ ] Выбор длины (слайдер)
- [ ] Выбор типов символов (заглавные, строчные, цифры, спецсимволы)
- [ ] Копирование в буфер обмена
- [ ] Показатель крепости пароля
- [ ] История последних паролей
- [ ] Копирование из истории
- [ ] Очистка истории
- [ ] Сохранение истории в браузер (LocalStorage)
- [ ] Красивый дизайн

**Бонусные фишки:**

- Экспорт в файл
- Фильтрация по типам символов
- Избегание похожих символов (0/O, l/1)
- Паролинг с паттернами (например, "слово + цифры")
- Проверка онлайн, кто-нибудь ли использует такой пароль

---

Отлично! Ты создал полезный инструмент для безопасности! 🔐
