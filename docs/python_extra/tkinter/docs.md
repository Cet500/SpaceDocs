# Мини‑документация по Tkinter (использованные элементы)

Здесь собраны основные элементы Tkinter, которые использовались в заданиях:

- Главное окно (`Tk`)
- Надпись (`Label`)
- Кнопка (`Button`)
- Поле ввода (`Entry`)
- Многострочный текст (`Text`)
- Контейнер (`Frame`)
- Менеджер размещения `pack`
- Изменение свойств (`config` / `cget`)
- Таймер и отложенный вызов (`after`)
- Базовое случайное поведение (через модуль `random`, совместно с Tkinter)

Примеры кода даны в самом простом, «учебном» стиле.

---

## 1. Главное окно: `Tk`

```python
import tkinter as tk


root = tk.Tk()  # создаём главное окно
root.title( "Заголовок окна" )  # текст в верхней полосе
root.geometry( "600x400" )  # размер: ширина x высота в пикселях

root.mainloop()  # запускаем цикл обработки событий
```

Основные методы:

- `title(text)` — установить заголовок окна.
- `geometry("ШxВ")` — задать размер окна.
- `config(опции...)` — изменить свойства окна (цвет фона и т.п.).
- `after(ms, func)` — выполнить функцию `func` через `ms` миллисекунд.

---

## 2. Надпись: `Label`

`Label` — простой виджет для отображения текста (и/или картинки). Нельзя нажать, он просто показывает информацию.

```python
label = tk.Label(
	root,
	text = "Привет, мир!",
	bg = "black",  # цвет фона
	fg = "white",  # цвет текста
	font = ("Arial", 14),  # шрифт, размер
	wraplength = 580,  # перенос строк по словам при достижении ширины
	justify = "left"  # выравнивание: left, center, right
)
label.pack( pady = 10 )
```

Часто используемые параметры:

- `text` — текст надписи.
- `bg` / `background` — цвет фона.
- `fg` / `foreground` — цвет текста.
- `font` — кортеж `(название_шрифта, размер[, стиль])`.
- `wraplength` — ширина (в пикселях), при превышении — перенос строки.
- `justify` — выравнивание текста.

Изменение текста:

```python
label.config( text = "Новый текст" )
```

Чтение текущего текста:

```python
current_text = label.cget( "text" )
```

---

## 3. Кнопка: `Button`

`Button` — виджет, который можно нажать. Важный параметр — `command`, указывающий, какую функцию вызвать при нажатии.

```python
def on_click():
	print( "Кнопка нажата" )


button = tk.Button(
	root,
	text = "Нажми меня",
	command = on_click,  # без скобок!
	bg = "gray",
	fg = "black"
)
button.pack( pady = 10 )
```

Состояния кнопки:

```python
button.config( state = "disabled" )  # отключить (серое, нажать нельзя)
button.config( state = "normal" )  # включить обратно
```

Частые случаи использования:

- Переход к следующей сцене.
- Реакция на выбор пользователя (ветвление истории).
- Запуск скримера/изменения интерфейса.

---

## 4. Поле ввода: `Entry`

`Entry` — однострочное поле, в которое пользователь может вводить текст.

Создание:

```python
entry = tk.Entry( root )
entry.pack( pady = 5 )
```

Чтение текста:

```python
text = entry.get()
```

Пример:

```python
def show_name():
	name = entry.get()
	label.config( text = f"Привет, {name}!" )


label = tk.Label( root, text = "Введите имя:" )
label.pack()

entry = tk.Entry( root )
entry.pack()

button = tk.Button( root, text = "OK", command = show_name )
button.pack()
```

---

## 5. Многострочный текст: `Text`

`Text` — многострочное текстовое поле. Подходит для длинных описаний, как в новеллах или пугалках.

Создание:

```python
text_widget = tk.Text(
	root,
	width = 70,  # ширина в символах
	height = 15,  # высота в строках
	wrap = "word"  # перенос по словам
)
text_widget.pack( pady = 10 )
```

Вставка текста:

```python
text_widget.insert( "1.0", "Первый текст" )  # "строка.символ"
```

Удаление текста:

```python
text_widget.delete( "1.0", "end" )
```

Режим только для чтения:

```python
text_widget.config( state = "disabled" )  # нельзя редактировать вручную

# чтобы обновить текст, нужно временно включить редактирование
text_widget.config( state = "normal" )
text_widget.delete( "1.0", "end" )
text_widget.insert( "1.0", "Новый текст" )
text_widget.config( state = "disabled" )
```

---

## 6. Контейнер: `Frame`

`Frame` — невидимый контейнер для других виджетов. Помогает группировать элементы и управлять размещением.

Простой пример:

```python
frame = tk.Frame( root, bg = "darkgray" )
frame.pack( pady = 10 )

label_left = tk.Label( frame, text = "Слева" )
label_left.pack( side = "left", padx = 5 )

label_right = tk.Label( frame, text = "Справа" )
label_right.pack( side = "left", padx = 5 )
```

Зачем нужен `Frame`:

- Располагает группу элементов в строку/столбец независимо от других частей окна.
- Упрощает управление сложными интерфейсами (разные панели, блоки).

---

## 7. Менеджер `pack`

`pack` — один из способов размещать виджеты в окне. Он укладывает элементы друг за другом (по вертикали или
горизонтали).

Базовый вызов:

```python
widget.pack()
```

Частые параметры:

- `side` — куда «приклеить» элемент: `"top"` (по умолчанию), `"bottom"`, `"left"`, `"right"`.
- `padx`, `pady` — внешние отступы по горизонтали и вертикали.
- `fill` — растягивание: `"x"`, `"y"` или `"both"`.
- `expand=True` — позволить виджету занимать свободное место.

Примеры:

```
# Вертикальный список виджетов
label1.pack(pady=5)
label2.pack(pady=5)

# Горизонтальное размещение внутри Frame
button1.pack(side="left", padx=5)
button2.pack(side="left", padx=5)
```

---

## 8. Изменение и чтение свойств: `config` и `cget`

Почти у всех виджетов есть:

- `.config(параметр=значение, ...)` — изменить настройки.
- `.cget("параметр")` — прочитать текущее значение.

Примеры:

```python
label.config( text = "Новый текст", fg = "red" )

current_text = label.cget( "text" )
print( current_text )
```

Часто в проектах:

- Меняется текст (`text`) в зависимости от сцены/комнаты.
- Меняется цвет (`fg`, `bg`) при скримере или страшной комнате.
- Меняется состояние кнопки (`state`).

---

## 9. Таймер и отложенные вызовы: `after`

`after` — метод окна или виджета, который позволяет выполнить функцию через указанный промежуток времени (в
миллисекундах).

```python
def hello():
	print( "Привет через 2 секунды" )


root.after( 2000, hello )  # 2000 мс = 2 секунды
```

В проектах‑пугалках:

- Используется, чтобы:
	- Показать скример с задержкой.
	- Вернуть обычный текст через какое‑то время.

Пример скримера:

```python
def show_jumpscare():
	old_text = label.cget( "text" )
	label.config( text = "!!! СКРИМЕР !!!", fg = "red" )
	root.after( 800, lambda: label.config( text = old_text, fg = "white" ) )
```

---

## 10. Модуль `random` (для случайностей)

Это уже не часть Tkinter, а стандартный модуль Python, который хорошо сочетается с GUI‑логикой.

```python
import random


if random.random() < 0.3:  # 30% вероятность
	print( "Событие произошло" )
```

В пугалке:

- Случайный шанс показать скример.
- Случайное время появления скримера:

```python
import random


delay = random.randint( 1000, 3000 )  # от 1 до 3 секунд
root.after( delay, show_jumpscare )
```

---

## 11. Общий шаблон программы на Tkinter

```python
import tkinter as tk


def main():
	root = tk.Tk()
	root.title( "Моё приложение" )
	root.geometry( "600x400" )

	# 1. создаём виджеты
	label = tk.Label( root, text = "Пример", fg = "white", bg = "black" )
	label.pack( pady = 10 )

	def on_click():
		label.config( text = "Нажали кнопку" )

	button = tk.Button( root, text = "Нажми", command = on_click )
	button.pack( pady = 10 )

	# 2. запускаем цикл
	root.mainloop()


if __name__ == "__main__":
	main()
```

Основные шаги всегда одинаковые:

1. Импортировать `tkinter`.
2. Создать главное окно (`Tk`).
3. Создать нужные виджеты (`Label`, `Button`, `Entry`, `Text`, `Frame`, ...).
4. Разместить их (`pack`, иногда `grid`).
5. Прописать функции‑обработчики.
6. Вызвать `mainloop()`.

На этой базе строятся и визуальные новеллы, и пугалки, и любые другие небольшие GUI‑приложения.
