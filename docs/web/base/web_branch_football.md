# ⚽ Проект: Сайт футбольной команды

## Идея проекта

Ты создашь настоящий сайт для своей вымышленной футбольной команды. На сайте будут:

- Главная страница с информацией о команде
- Страница с игроками
- Расписание матчей
- Галерея с фото
- Контакты

**Важно:** Это простой проект. Ты не должен знать абсолютно всё, чтобы его делать. Можешь учиться прямо во время
разработки.

**Навыки, которые тренируются:**

- Структурирование сайта (несколько страниц)
- HTML-формы (контакты)
- CSS-раскладка (таблицы с игроками)
- Картинки и медиа
- Простая навигация

---

## Модуль 1: Структура проекта

### Задание 1.1: Создаём папку проекта и основные файлы

**Что мы делаем:**
Создаём папку для всего проекта и несколько HTML-файлов.

**Структура проекта:**

```
my-football-team/
├── index.html          (главная страница)
├── players.html        (страница с игроками)
├── schedule.html       (расписание матчей)
├── gallery.html        (галерея фото)
├── contacts.html       (контакты)
├── style.css           (стили для всех страниц)
└── images/             (папка с картинками)
```

**Что мы делаем:**

1. Создай папку `my-football-team`.
2. Внутри создай файлы: `index.html`, `players.html`, `schedule.html`, `gallery.html`, `contacts.html`, `style.css`.
3. Создай папку `images` для картинок.

**Пример кода для `index.html`:**

```html
<html>
  <head>
    <title>FC Dragon - футбольная команда</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <nav class="navbar">
      <div class="logo">⚽ FC Dragon</div>
      <ul class="menu">
        <li><a href="index.html">Главная</a></li>
        <li><a href="players.html">Игроки</a></li>
        <li><a href="schedule.html">Матчи</a></li>
        <li><a href="gallery.html">Галерея</a></li>
        <li><a href="contacts.html">Контакты</a></li>
      </ul>
    </nav>

    <header class="hero">
      <h1>FC Dragon</h1>
      <p>Лучшая команда в городе</p>
    </header>

    <main>
      <section class="info">
        <h2>О команде</h2>
        <p>Мы — молодая и энергичная команда, основанная в 2020 году. Наша цель — играть в красивый футбол и выигрывать турниры!</p>
      </section>
    </main>

    <footer>
      <p>© 2024 FC Dragon. Все права защищены.</p>
    </footer>
  </body>
</html>
```

**Что попробовать:**

1. Создай все файлы, откройте `index.html` в браузере.
2. Нажми на ссылку "Игроки" — перейдёшь ли на `players.html`? (Пока там ничего нет, но навигация работает.)
3. Добавь своё название команды вместо "FC Dragon".

---

## Модуль 2: Главная страница

### Задание 2.1: Красивая главная страница с информацией

**Что мы делаем:**
Создаём впечатляющую главную страницу с описанием команды и основной информацией.

**Пример HTML (`index.html`):**

```html
<html>
  <head>
    <title>FC Dragon - футбольная команда</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <nav class="navbar">
      <div class="logo">⚽ FC Dragon</div>
      <ul class="menu">
        <li><a href="index.html">Главная</a></li>
        <li><a href="players.html">Игроки</a></li>
        <li><a href="schedule.html">Матчи</a></li>
        <li><a href="gallery.html">Галерея</a></li>
        <li><a href="contacts.html">Контакты</a></li>
      </ul>
    </nav>

    <header class="hero">
      <h1>⚽ FC Dragon</h1>
      <p>Лучшая команда в городе!</p>
      <button class="cta-button">Смотреть матчи</button>
    </header>

    <main>
      <section class="info">
        <h2>О команде</h2>
        <p>Мы — молодая и энергичная команда, основанная в 2020 году. Наша цель — играть в красивый футбол и выигрывать турниры!</p>
        
        <div class="team-stats">
          <div class="stat-box">
            <div class="stat-number">15</div>
            <div class="stat-label">Игроков</div>
          </div>
          <div class="stat-box">
            <div class="stat-number">5</div>
            <div class="stat-label">Побед подряд</div>
          </div>
          <div class="stat-box">
            <div class="stat-number">1-е</div>
            <div class="stat-label">Место в лиге</div>
          </div>
        </div>
      </section>

      <section class="highlights">
        <h2>Последние новости</h2>
        <article class="news-card">
          <h3>Победа 3:1!</h3>
          <p>Вчера наша команда одержала блестящую победу против соседей. Великолепная игра в защите и опасные атаки!</p>
        </article>
        <article class="news-card">
          <h3>Новичок присоединился</h3>
          <p>Рады представить нового полузащитника, который недавно присоединился к нашей команде. Играет в классе 6/10!</p>
        </article>
      </section>
    </main>

    <footer>
      <p>© 2024 FC Dragon. Все права защищены.</p>
    </footer>
  </body>
</html>
```

**Пример CSS (`style.css`):**

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  color: #333;
}

/* Навигация */
.navbar {
  background-color: #1a1a2e;
  padding: 15px 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: sticky;
  top: 0;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.logo {
  color: #00d4ff;
  font-size: 24px;
  font-weight: bold;
}

.menu {
  display: flex;
  list-style: none;
  gap: 30px;
}

.menu a {
  color: white;
  text-decoration: none;
  transition: color 0.3s;
}

.menu a:hover {
  color: #00d4ff;
}

/* Герой-секция */
.hero {
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
  color: white;
  padding: 100px 20px;
  text-align: center;
}

.hero h1 {
  font-size: 48px;
  margin-bottom: 20px;
}

.hero p {
  font-size: 20px;
  margin-bottom: 30px;
}

.cta-button {
  background-color: #00d4ff;
  color: #1a1a2e;
  padding: 12px 30px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
  transition: all 0.3s;
}

.cta-button:hover {
  background-color: #0099cc;
  transform: scale(1.05);
}

/* Основной контент */
main {
  max-width: 1000px;
  margin: 0 auto;
  padding: 40px 20px;
}

.info h2, .highlights h2 {
  font-size: 32px;
  margin-bottom: 20px;
  color: #1a1a2e;
}

.info p {
  font-size: 16px;
  margin-bottom: 30px;
  color: #666;
}

/* Статистика */
.team-stats {
  display: flex;
  gap: 20px;
  margin-top: 30px;
  justify-content: center;
  flex-wrap: wrap;
}

.stat-box {
  background-color: #f5f5f5;
  padding: 30px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.stat-box:hover {
  transform: translateY(-5px);
}

.stat-number {
  font-size: 36px;
  font-weight: bold;
  color: #00d4ff;
}

.stat-label {
  font-size: 14px;
  color: #666;
  margin-top: 10px;
}

/* Новости */
.highlights {
  margin-top: 60px;
}

.news-card {
  background-color: white;
  border-left: 4px solid #00d4ff;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s;
}

.news-card:hover {
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  transform: translateX(5px);
}

.news-card h3 {
  color: #1a1a2e;
  margin-bottom: 10px;
}

.news-card p {
  color: #666;
}

/* Футер */
footer {
  background-color: #1a1a2e;
  color: white;
  text-align: center;
  padding: 20px;
  margin-top: 60px;
}
```

**Что попробовать:**

1. Измени цвета: `#1a1a2e` на другой цвет (например, `#333333`).
2. Добавь больше статистики в `.team-stats`.
3. Добавь больше новостей в `.highlights`.

---

## Модуль 3: Страница с игроками

### Задание 3.1: Таблица и карточки игроков

**Что мы делаем:**
Создаём страницу с информацией о каждом игроке команды.

**Пример HTML (`players.html`):**

```html
<html>
  <head>
    <title>Игроки - FC Dragon</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <nav class="navbar">
      <div class="logo">⚽ FC Dragon</div>
      <ul class="menu">
        <li><a href="index.html">Главная</a></li>
        <li><a href="players.html">Игроки</a></li>
        <li><a href="schedule.html">Матчи</a></li>
        <li><a href="gallery.html">Галерея</a></li>
        <li><a href="contacts.html">Контакты</a></li>
      </ul>
    </nav>

    <main>
      <h1>Наша команда</h1>
      
      <section class="players-grid">
        <div class="player-card">
          <div class="player-number">1</div>
          <h3>Иван Петров</h3>
          <p class="position">Вратарь</p>
          <p class="description">Опытный вратарь с 10-летним стажем. Никогда не пропускает гол!</p>
          <div class="player-stats">
            <span>Матчи: 45</span>
            <span>Чистые листы: 20</span>
          </div>
        </div>

        <div class="player-card">
          <div class="player-number">4</div>
          <h3>Алексей Сидоров</h3>
          <p class="position">Защитник</p>
          <p class="description">Быстрый и надёжный защитник. Лидер нашей обороны.</p>
          <div class="player-stats">
            <span>Матчи: 42</span>
            <span>Голы: 3</span>
          </div>
        </div>

        <div class="player-card">
          <div class="player-number">7</div>
          <h3>Сергей Волков</h3>
          <p class="position">Полузащитник</p>
          <p class="description">Творческий полузащитник. Делает отличные передачи!</p>
          <div class="player-stats">
            <span>Матчи: 38</span>
            <span>Голы: 5</span>
          </div>
        </div>

        <div class="player-card">
          <div class="player-number">9</div>
          <h3>Максим Орлов</h3>
          <p class="position">Нападающий</p>
          <p class="description">Лучший бомбардир команды. Забивает в каждом матче!</p>
          <div class="player-stats">
            <span>Матчи: 40</span>
            <span>Голы: 18</span>
          </div>
        </div>

        <div class="player-card">
          <div class="player-number">10</div>
          <h3>Дмитрий Соколов</h3>
          <p class="position">Полузащитник</p>
          <p class="description">Капитан команды. Вдохновляет всех своей игрой.</p>
          <div class="player-stats">
            <span>Матчи: 44</span>
            <span>Голы: 8</span>
          </div>
        </div>

        <div class="player-card">
          <div class="player-number">15</div>
          <h3>Павел Ковалев</h3>
          <p class="position">Защитник</p>
          <p class="description">Молодой перспективный защитник. Будущее команды!</p>
          <div class="player-stats">
            <span>Матчи: 20</span>
            <span>Голы: 0</span>
          </div>
        </div>
      </section>
    </main>

    <footer>
      <p>© 2024 FC Dragon. Все права защищены.</p>
    </footer>
  </body>
</html>
```

**Добавь в CSS (`style.css`):**

```css
/* Страница игроков */
main h1 {
  text-align: center;
  font-size: 36px;
  margin: 40px 0 30px;
  color: #1a1a2e;
}

.players-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.player-card {
  background-color: white;
  border: 2px solid #00d4ff;
  border-radius: 8px;
  padding: 20px;
  width: 280px;
  text-align: center;
  transition: all 0.3s;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.player-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  border-color: #0099cc;
}

.player-number {
  font-size: 48px;
  font-weight: bold;
  color: #00d4ff;
  margin-bottom: 10px;
}

.player-card h3 {
  font-size: 20px;
  color: #1a1a2e;
  margin-bottom: 5px;
}

.position {
  font-weight: bold;
  color: #00d4ff;
  margin-bottom: 10px;
}

.description {
  color: #666;
  font-size: 14px;
  margin-bottom: 15px;
}

.player-stats {
  display: flex;
  gap: 10px;
  flex-direction: column;
  font-size: 13px;
  color: #666;
}

/* Адаптивность */
@media (max-width: 768px) {
  .players-grid {
    gap: 15px;
  }

  .player-card {
    width: calc(50% - 8px);
  }
}

@media (max-width: 480px) {
  .player-card {
    width: 100%;
  }
}
```

**Что попробовать:**

1. Добавь ещё 3-4 игроков в таблицу.
2. Измени номера и позиции игроков.
3. Добавь свои имена вместо примеров.

---

## Модуль 4: Расписание матчей

### Задание 4.1: Таблица с матчами

**Что мы делаем:**
Создаём страницу с расписанием предстоящих матчей.

**Пример HTML (`schedule.html`):**

```html
<html>
  <head>
    <title>Расписание - FC Dragon</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <nav class="navbar">
      <div class="logo">⚽ FC Dragon</div>
      <ul class="menu">
        <li><a href="index.html">Главная</a></li>
        <li><a href="players.html">Игроки</a></li>
        <li><a href="schedule.html">Матчи</a></li>
        <li><a href="gallery.html">Галерея</a></li>
        <li><a href="contacts.html">Контакты</a></li>
      </ul>
    </nav>

    <main>
      <h1>Расписание матчей</h1>
      
      <table class="schedule-table">
        <thead>
          <tr>
            <th>Дата</th>
            <th>Время</th>
            <th>Противник</th>
            <th>Место</th>
            <th>Результат</th>
          </tr>
        </thead>
        <tbody>
          <tr class="upcoming">
            <td>15.01.2025</td>
            <td>18:00</td>
            <td>ФК Звёзды</td>
            <td>Стадион "Дракон"</td>
            <td>Предстоит</td>
          </tr>
          <tr class="upcoming">
            <td>22.01.2025</td>
            <td>19:30</td>
            <td>ФК Орлы</td>
            <td>Стадион "Орлиное гнездо"</td>
            <td>Предстоит</td>
          </tr>
          <tr class="completed">
            <td>08.01.2025</td>
            <td>18:00</td>
            <td>ФК Тигры</td>
            <td>Стадион "Дракон"</td>
            <td class="result-win">3:1 ✓</td>
          </tr>
          <tr class="completed">
            <td>01.01.2025</td>
            <td>15:00</td>
            <td>ФК Львы</td>
            <td>Стадион "Львы"</td>
            <td class="result-win">2:0 ✓</td>
          </tr>
          <tr class="completed">
            <td>25.12.2024</td>
            <td>16:00</td>
            <td>ФК Пантеры</td>
            <td>Стадион "Дракон"</td>
            <td class="result-draw">1:1 =</td>
          </tr>
        </tbody>
      </table>
    </main>

    <footer>
      <p>© 2024 FC Dragon. Все права защищены.</p>
    </footer>
  </body>
</html>
```

**Добавь в CSS (`style.css`):**

```css
/* Таблица расписания */
.schedule-table {
  max-width: 1000px;
  margin: 30px auto;
  width: 100%;
  border-collapse: collapse;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.schedule-table thead {
  background-color: #1a1a2e;
  color: white;
}

.schedule-table th {
  padding: 15px;
  text-align: left;
  font-weight: bold;
}

.schedule-table td {
  padding: 15px;
  border-bottom: 1px solid #ddd;
}

.schedule-table tbody tr {
  transition: background-color 0.3s;
}

.schedule-table tbody tr:hover {
  background-color: #f9f9f9;
}

.upcoming {
  background-color: #f0f8ff;
}

.completed {
  background-color: #f5f5f5;
}

.result-win {
  color: green;
  font-weight: bold;
}

.result-draw {
  color: orange;
  font-weight: bold;
}

@media (max-width: 768px) {
  .schedule-table {
    font-size: 14px;
  }

  .schedule-table th,
  .schedule-table td {
    padding: 10px;
  }
}
```

**Что попробовать:**

1. Добавь ещё матчей в таблицу (прошлых и будущих).
2. Добавь третий результат: поражение (с классом `.result-loss` и красным цветом).
3. Измени даты и время.

---

## Модуль 5: Галерея фото

### Задание 5.1: Галерея с картинками команды

**Что мы делаем:**
Создаём красивую галерею фото с эффектами.

**Пример HTML (`gallery.html`):**

```html
<html>
  <head>
    <title>Галерея - FC Dragon</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <nav class="navbar">
      <div class="logo">⚽ FC Dragon</div>
      <ul class="menu">
        <li><a href="index.html">Главная</a></li>
        <li><a href="players.html">Игроки</a></li>
        <li><a href="schedule.html">Матчи</a></li>
        <li><a href="gallery.html">Галерея</a></li>
        <li><a href="contacts.html">Контакты</a></li>
      </ul>
    </nav>

    <main>
      <h1>Галерея команды</h1>
      
      <div class="gallery">
        <div class="gallery-item">
          <img src="images/team-photo.jpg" alt="Фото команды">
          <div class="gallery-caption">Командное фото</div>
        </div>
        <div class="gallery-item">
          <img src="images/match1.jpg" alt="Матч 1">
          <div class="gallery-caption">Матч против ФК Тигры</div>
        </div>
        <div class="gallery-item">
          <img src="images/match2.jpg" alt="Матч 2">
          <div class="gallery-caption">Атака Максима Орлова</div>
        </div>
        <div class="gallery-item">
          <img src="images/training.jpg" alt="Тренировка">
          <div class="gallery-caption">Тренировка на стадионе</div>
        </div>
        <div class="gallery-item">
          <img src="images/celebration.jpg" alt="Празднование">
          <div class="gallery-caption">Празднование победы</div>
        </div>
        <div class="gallery-item">
          <img src="images/fans.jpg" alt="Болельщики">
          <div class="gallery-caption">Наши верные фанаты</div>
        </div>
      </div>
    </main>

    <footer>
      <p>© 2024 FC Dragon. Все права защищены.</p>
    </footer>
  </body>
</html>
```

**Добавь в CSS (`style.css`):**

```css
/* Галерея */
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  max-width: 1200px;
  margin: 30px auto;
  padding: 20px;
}

.gallery-item {
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s;
}

.gallery-item:hover {
  transform: scale(1.05);
}

.gallery-item img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  display: block;
}

.gallery-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 15px;
  text-align: center;
  font-size: 14px;
  transform: translateY(100%);
  transition: transform 0.3s;
}

.gallery-item:hover .gallery-caption {
  transform: translateY(0);
}
```

**Что попробовать:**

1. Добавь больше фото в галерею.
2. Добавь более длинные описания для фото.
3. Измени размер сетки: `grid-template-columns: repeat(4, 1fr);`.

---

## Модуль 6: Страница контактов с формой

### Задание 6.1: Форма для связи

**Что мы делаем:**
Создаём страницу с контактами и формой обратной связи.

**Пример HTML (`contacts.html`):**

```html
<html>
  <head>
    <title>Контакты - FC Dragon</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <nav class="navbar">
      <div class="logo">⚽ FC Dragon</div>
      <ul class="menu">
        <li><a href="index.html">Главная</a></li>
        <li><a href="players.html">Игроки</a></li>
        <li><a href="schedule.html">Матчи</a></li>
        <li><a href="gallery.html">Галерея</a></li>
        <li><a href="contacts.html">Контакты</a></li>
      </ul>
    </nav>

    <main>
      <h1>Свяжись с нами</h1>
      
      <div class="contacts-container">
        <div class="contact-info">
          <h2>Информация</h2>
          <p><strong>Адрес:</strong> ул. Футбольная, 42, г. Москва</p>
          <p><strong>Телефон:</strong> +7 (999) 123-45-67</p>
          <p><strong>Email:</strong> info@fcdragon.ru</p>
          <p><strong>Время работы:</strong> Пн-Пт: 10:00-18:00</p>
        </div>

        <form class="contact-form">
          <div class="form-group">
            <label for="name">Твоё имя</label>
            <input type="text" id="name" name="name" required>
          </div>

          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" name="email" required>
          </div>

          <div class="form-group">
            <label for="message">Сообщение</label>
            <textarea id="message" name="message" rows="5" required></textarea>
          </div>

          <button type="submit" class="submit-button">Отправить</button>
        </form>
      </div>
    </main>

    <footer>
      <p>© 2024 FC Dragon. Все права защищены.</p>
    </footer>
  </body>
</html>
```

**Добавь в CSS (`style.css`):**

```css
/* Контакты */
.contacts-container {
  display: flex;
  gap: 40px;
  max-width: 1000px;
  margin: 30px auto;
  padding: 20px;
}

.contact-info {
  flex: 1;
  background-color: #f5f5f5;
  padding: 30px;
  border-radius: 8px;
}

.contact-info h2 {
  color: #1a1a2e;
  margin-bottom: 20px;
}

.contact-info p {
  margin-bottom: 15px;
  color: #666;
}

.contact-form {
  flex: 1;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  color: #1a1a2e;
  font-weight: bold;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  font-family: Arial, sans-serif;
  transition: border-color 0.3s;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #00d4ff;
}

.submit-button {
  background-color: #00d4ff;
  color: #1a1a2e;
  padding: 12px 30px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: all 0.3s;
  width: 100%;
}

.submit-button:hover {
  background-color: #0099cc;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

@media (max-width: 768px) {
  .contacts-container {
    flex-direction: column;
    gap: 20px;
  }
}
```

**Что попробовать:**

1. Добавь больше полей в форму (например, телефон, сообщение).
2. Добавь валидацию (покажи сообщение об ошибке, если поле пусто).
3. Измени цвет кнопки.

---

## Итоговая проверка

**Задание:** Проверь, что всё работает:

- [ ] Навигация работает на всех страницах
- [ ] Главная страница красивая и информативная
- [ ] Страница игроков показывает всех игроков
- [ ] Расписание показывает матчи (прошлые и будущие)
- [ ] Галерея показывает фото (или хотя бы ссылки на фото)
- [ ] Форма контактов заполняется
- [ ] Всё хорошо выглядит на компьютере
- [ ] Всё хорошо выглядит на телефоне (сожми окно браузера)
- [ ] Цвета и стили единообразны

Если всё работает — поздравляем! Ты создал настоящий сайт! 🎉

---

## Бонусные фишки (если хочешь продолжить)

1. **Добавь JavaScript** для интерактивности:
	- Показывай/скрывай информацию при клике
	- Добавь фильтр для игроков по позиции
	- Сделай поиск по матчам

2. **Улучши галерею:**
	- Добавь модальное окно (лайтбокс) для просмотра фото в большом размере
	- Добавь категории фото (матчи, тренировки, события)

3. **Добавь анимации:**
	- Анимируй счётчики статистики (0 → 15)
	- Добавь анимацию загрузки страницы
	- Сделай плавный скролл

4. **Улучши дизайн:**
	- Добавь логотип команды (SVG или картинка)
	- Сделай тёмный режим
	- Добавь живой чат или чат-бот

Успехов! 🚀
