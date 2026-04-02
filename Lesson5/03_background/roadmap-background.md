# Властивості background у CSS

## Зміст
1. [Вступ](#вступ)
2. [Основні властивості background](#основні-властивості-background)
3. [Комплексна властивість background](#комплексна-властивість-background)
4. [Практичні приклади](#практичні-приклади)
5. [Поради та трюки](#поради-та-трюки)

## Вступ
Властивості `background` в CSS використовуються для стилізації фону елементів. Вони дозволяють налаштувати колір, зображення, повторення, позиціонування та інші параметри фону. У цій лекції ми детально розглянемо кожну властивість та навчимося їх ефективно використовувати.

## Основні властивості background

### 1. background-color
Задає колір фону елемента.

```css
.element {
  background-color: red;
  /* Можливі значення: */
  background-color: #ff0000;         /* HEX */
  background-color: rgb(255, 0, 0);  /* RGB */
  background-color: rgba(255, 0, 0, 0.5); /* RGBA з прозорістю */
  background-color: transparent;      /* Прозорий фон */
}
```

### 2. background-image
Встановлює фонове зображення.

```css
.element {
  background-image: url('images/image.jpg');
  /* Можливі варіанти: */
  background-image: linear-gradient(to right, red, blue); /* Градієнт */
  background-image: none; /* Без зображення */
  /* Можна вказати декілька зображень через кому */
  background-image: url('image1.jpg'), url('image2.jpg');
}
```

### 3. background-repeat
Визначає, як буде повторюватися фонове зображення.

```css
.element {
  background-repeat: no-repeat;
  /* Інші значення: */
  background-repeat: repeat;      /* Повторення по X та Y */
  background-repeat: repeat-x;    /* Повторення тільки по горизонталі */
  background-repeat: repeat-y;    /* Повторення тільки по вертикалі */
  background-repeat: space;       /* Повторення з рівними проміжками */
  background-repeat: round;       /* Повторення з масштабуванням */
}
```

### 4. background-position
Встановлює початкову позицію фонового зображення.

```css
.element {
  background-position: center;
  /* Можливі значення: */
  background-position: top;
  background-position: bottom;
  background-position: left;
  background-position: right;
  background-position: 50% 50%;   /* У відсотках */
  background-position: 20px 30px; /* У пікселях */
}
```

### 5. background-size
Визначає розмір фонового зображення.

```css
.element {
  background-size: cover;
  /* Інші варіанти: */
  background-size: contain;     /* Вписує зображення повністю */
  background-size: 100% 100%;   /* У відсотках */
  background-size: 300px auto;  /* Конкретні розміри */
  background-size: auto;        /* Оригінальний розмір */
}
```

### 6. background-attachment
Визначає, чи буде фонове зображення прокручуватися разом із вмістом.

```css
.element {
  background-attachment: fixed;
  /* Можливі значення: */
  background-attachment: scroll; /* Прокручується зі сторінкою */
  background-attachment: local;  /* Прокручується з елементом */
}
```

## Комплексна властивість background

Всі вищезгадані властивості можна об'єднати в одну:

```css
.element {
  background: url('images/image.jpg') no-repeat center/cover;
  
  /* Це те саме, що: */
  background-image: url('images/image.jpg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
```

## Практичні приклади

### Приклад 1: Герой-секція з фоновим зображенням
```css
.hero {
  min-height: 100vh;
  background: url('hero-bg.jpg') no-repeat center/cover;
  padding: 50px;
  color: white;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### Приклад 2: Градієнтний фон
```css
.gradient-bg {
  background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
  /* або багатокольоровий градієнт */
  background: linear-gradient(to right, #ff6b6b, #4ecdc4, #45b649);
}
```

### Приклад 3: Напівпрозорий фон
```css
.overlay {
  background: rgba(0, 0, 0, 0.7);
  /* або з використанням градієнта */
  background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)),
              url('background.jpg') no-repeat center/cover;
}
```

## Поради та трюки

### 1. Оптимізація продуктивності
- Використовуйте оптимізовані зображення
- Застосовуйте WebP формат з fallback
- Уникайте великих фонових зображень на мобільних пристроях

```css
/* Приклад адаптивного фону */
.responsive-bg {
  background-image: url('mobile-bg.jpg');
}

@media (min-width: 768px) {
  .responsive-bg {
    background-image: url('desktop-bg.jpg');
  }
}
```

### 2. Множинні фони
```css
.multiple-backgrounds {
  background: 
    url('overlay.png'),
    url('pattern.png'),
    url('background.jpg');
  background-position: 
    center center,
    top left,
    center center;
}
```

### 3. Паралакс ефект
```css
.parallax {
  background: url('parallax-bg.jpg') no-repeat center fixed;
  background-size: cover;
  min-height: 500px;
}
```

## Поширені помилки та як їх уникнути

1. **Неоптимізовані зображення**
   - Завжди оптимізуйте зображення перед використанням
   - Використовуйте відповідні формати (JPG для фотографій, PNG для прозорості)

2. **Неправильне використання background-size**
   - `cover` може обрізати частину зображення
   - `contain` може залишити порожній простір
   - Вибирайте значення відповідно до дизайну

3. **Забування про мобільні пристрої**
   - Завжди тестуйте на різних розмірах екрану
   - Використовуйте медіа-запити для адаптації фону

## Висновок
Властивості `background` надають потужні можливості для стилізації веб-сторінок. Правильне використання цих властивостей дозволяє створювати привабливі та функціональні дизайни. Пам'ятайте про оптимізацію та адаптивність при роботі з фоновими зображеннями.
