# Модуль 20. Стандарты написания кода и общие подходы

## 20.10. Практическая работа

---

## 📌 Задание на 10 баллов

**Требуется:** улучшить код с точки зрения DRY, KISS, YAGNI, SOLID. По каждому из принципов сделать как минимум одно исправление.

---

### 1. DRY (Don't Repeat Yourself)

Выявлены повторяющиеся стили у кнопок и чекбоксов разных секций, вынесены в общие стили в начало файла `style.css` (можно переиспользовать).

---

### 2. KISS (Keep It Simple, Stupid)

#### 2.1. Названия классов изменены на интуитивно более понятные

###### Пример

_Исходный код:_

```
css

.gold-text {
 color: #e3b873;
}
```

_Улучшенный код:_

```
.hero__title--gold {
 color: #e3b873;
}
```

#### 2.2 Упрощен код кнопок секции Hero.

_Исходный код:_

```
.hero-buttons .button {
 margin-right: 20px;
}

.hero-buttons .button:last-child {
 background: transparent;
 border: 1px solid white;
 box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
 box-sizing: border-box;
 padding: 12px 32px;
}
```

_Улучшенный код:_

```
.hero__actions {
 display: flex;
 gap: 20px;
}

.button--submit {
 background: transparent;
 border: 1px solid white;
 box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
 box-sizing: border-box;
 padding: 12px 32px;
}
```

#### 2.3 Создан общий класс карточек секции TYPES OF REPAIR и отдельно вынесены картинки.

_Исходный код:_

```
.block-redecorating {
 max-width: 392px;
 height: 421px;
 padding-left: 31px;
 padding-right: 31px;
 background: center no-repeat url("../images/redecorating.png");
 background-size: cover;
}

.block-overhaul {
 max-width: 392px;
 height: 421px;
 padding-left: 31px;
 padding-right: 31px;
 background: center no-repeat url("../images/overhaul.png");
 background-size: cover;
}

.block-designer-repair {
 max-width: 392px;
 height: 421px;
 padding-left: 31px;
 padding-right: 31px;
 background: center no-repeat url("../images/designer-repair.png");
 background-size: cover;
}
```

_Улучшенный код:_

```
/_ Общие стили _/
.repair-card {
 max-width: 392px;
 height: 421px;
 padding-left: 31px;
 padding-right: 31px;
 background-size: cover;
 background-position: center;
 background-repeat: no-repeat;
}

/_ картинки отдельно _/
.repair-card--redecorating {
 background-image: url("../images/redecorating.png");
}

.repair-card--overhaul {
 background-image: url("../images/overhaul.png");
}

.repair-card--designer {
 background-image: url("../images/designer-repair.png");
}
```

### 3. YAGNI

---

_Пример._ Не добавлялась форма поиска по сайту, ее не было в макете.

### 4. SOLID

---

В основном проекте:

- разделение задач в CSS (общий container с шириной и центрированием и контейнеры для секций с раскладкой элементов).
- В секции Hero добавлен модификатор .button--submit, который расширяет базовый класс .button. Новые варианты кнопок можно добавлять, не меняя существующий код.
- Все модификаторы кнопки могут использоваться в любом месте вместо базовой, сохраняя все ее свойства.

Для принципов, которые не удается показать на примере сайта, используется исходный код из задания к модулю 6. Старт в JavaScript (https://github.com/Ju17-art/js-start/blob/main/task2/script.js):

```
// Обработчик для console.log

const consoleLog = document.querySelector('#consoleLog');

consoleLog.addEventListener('click', () => {
    alert('Служит для вывода информации в консоль');
});

// Обработчик для alert

const alertExample = document.querySelector('#alert');
alertExample.addEventListener('click', () => {
     alert('Показывает диалоговое окно с сообщением и кнопкой OK');
});

// Обработчик для prompt

const promptExample = document.querySelector('#prompt');
promptExample.addEventListener('click', () => {
    alert('Отображает диалоговое окно с запросом на ввод текста');
});
```

_Улучшенный код:_

#### 1. S - Single Responsibility (одна функция - одна задача)

```
const findElement = (selector) => document.querySelector(selector);
const showAlert = (message) => alert(message);
const bindClick = (element, handler) =>
element.addEventListener("click", handler);
```

#### 2. O - Open/Closed (открыт для расширения)

```
const descriptions = {
"#consoleLog": "Служит для вывода информации в консоль",
"#alert": "Показывает диалоговое окно с сообщением и кнопкой OK",
"#prompt": "Отображает диалоговое окно с запросом на ввод текста",
// Можно добавить новые без изменения кода
};
```

#### 3. L - Liskov (все элементы обрабатываются одинаково)

```
Object.entries(descriptions).forEach(([selector, message]) => {
const element = findElement(selector);
bindClick(element, () => showAlert(message));
});
```

#### 4. I - Interface Segregation (используются только нужные функции)

Отдельные функции вместо одного большого объекта.

#### 5. D - Dependency Inversion (не зависит от абстракций)

Функции принимают абстрактные параметры, не привязаны к конкретным значениям.

## 📌 Задание на 15 баллов

**Требуется:** проверить семантику и валидность верстки сайта для проекта Repair Design Project.

### 1. Семантика.

- Использованы семантические теги: &lt;header&gt;, &lt;nav&gt;, &lt;main&gt;, &lt;section&gt;, &lt;article&gt;, &lt;footer&gt;
- Соблюдена иерархия заголовков: &lt;h1&gt; → &lt;h2&gt; → &lt;h3&gt;
- Формы обернуты в &lt;form&gt;, поля ввода — &lt;input&gt; с типами text, tel, email, подписи полей - &lt;label&gt;
- Все кнопки выполнены тегом &lt;button&gt;
- Списки навигации и преимуществ оформлены через &lt;ul&gt; / &lt;li&gt;

### 2. Валидность.

- Код проверен на сайте https://validator.w3.org/
- Предупреждения валидатора не являются критическими и не влияют на отображение
- Все теги закрыты, вложенность соблюдена
- Отсутствуют устаревшие атрибуты
- Использованы правильные типы полей в формах (text, tel, email)
- Изображения имеют атрибут alt

## 📌 Задание на 20 баллов

**Требуется:** выполнить (доработать) верстку по БЭМ. Использовать линтеры (указать, какие именно) для проверки кода на наличие ошибок и приведения его в порядок.

### Проект из модуля 18

https://github.com/Ju17-art/repair-design-project/

https://ju17-art.github.io/repair-design-project/

### Доработанный проект

https://github.com/Ju17-art/design-project-bem/

https://ju17-art.github.io/design-project-bem/

---

#### ЛИНТЕРЫ

Stylelint, HTMLHint, ESLint, а также Prettier.
