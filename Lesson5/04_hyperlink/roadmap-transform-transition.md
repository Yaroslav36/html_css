# CSS Переходи та Трансформації

## 1. Трансформації (transform)

### 1.1. Основні функції transform

#### Translate (переміщення)

- `translateX()` - горизонтальне переміщення
- `translateY()` - вертикальне переміщення
- `translate()` - переміщення по обох осях

```css
.element {
  transform: translateX(100px); /* зміщення вправо на 100px */
  transform: translateY(-50px); /* зміщення вгору на 50px */
  transform: translate(100px, 50px); /* зміщення вправо та вниз */
}
```

#### Scale (масштабування)

- `scaleX()` - масштабування по горизонталі
- `scaleY()` - масштабування по вертикалі
- `scale()` - масштабування по обох осях

```css
.element {
  transform: scaleX(2); /* розтягнення вдвічі по горизонталі */
  transform: scaleY(0.5); /* зменшення вдвічі по вертикалі */
  transform: scale(2); /* збільшення вдвічі по обох осях */
  transform: scale(-1); /* дзеркальне відображення */
}
```

#### Rotate (обертання)

```css
.element {
  transform: rotate(45deg); /* обертання на 45 градусів за годинниковою */
  transform: rotate(-90deg); /* обертання на 90 градусів проти годинникової */
  transform: rotate(0.5turn); /* обертання на пів оберта */
}
```

#### Skew (нахил)

```css
.element {
  transform: skewX(20deg); /* нахил по горизонталі */
  transform: skewY(10deg); /* нахил по вертикалі */
  transform: skew(20deg, 10deg); /* нахил по обох осях */
}
```

### 1.2. Комбінування трансформацій

```css
.element {
  transform: translate(100px, 50px) rotate(45deg) scale(1.5);
}
```

### 1.3. Точка трансформації

```css
.element {
  transform-origin: left top; /* точка трансформації у верхньому лівому куті */
  transform-origin: center; /* точка трансформації в центрі (за замовчуванням) */
  transform-origin: 100% 100%; /* точка трансформації в правому нижньому куті */
}
```

## 2. Переходи (transition)

### 2.1. Властивості переходу

- `transition-property` - властивість, яка анімується
- `transition-duration` - тривалість переходу
- `transition-timing-function` - функція часу
- `transition-delay` - затримка перед початком

```css
.element {
  /* Окремі властивості */
  transition-property: transform;
  transition-duration: 0.3s;
  transition-timing-function: ease;
  transition-delay: 0s;

  /* Скорочений запис */
  transition: transform 0.3s ease 0s;
}
```

### 2.2. Функції часу (timing functions)

```css
.element {
  transition-timing-function: linear; /* рівномірна швидкість */
  transition-timing-function: ease; /* плавний початок і кінець */
  transition-timing-function: ease-in; /* плавний початок */
  transition-timing-function: ease-out; /* плавний кінець */
  transition-timing-function: ease-in-out; /* плавний початок і кінець */
  transition-timing-function: cubic-bezier(
    0.1,
    0.7,
    1,
    0.1
  ); /* користувацька */
}
```

## 3. Практичні приклади

### 3.1. Кнопка з ефектом наведення

```html
<button class="button">Натисни мене</button>
```

```css
.button {
  padding: 10px 20px;
  background: #007bff;
  border: none;
  border-radius: 4px;
  color: white;
  transition: all 0.2s ease;
}

.button:hover {
  transform: scale(1.1);
  background: #0056b3;
}
```

### 3.2. Картка з ефектом підйому

```html
<div class="card">
  <h3>Заголовок картки</h3>
  <p>Текст картки</p>
</div>
```

```css
.card {
  padding: 20px;
  background: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.card:hover {
  transform: translateY(10px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}
```

### 3.3. Меню з плавним підкресленням

```html
<nav>
  <a href="#" class="menu-item">Головна</a>
  <a href="#" class="menu-item">Про нас</a>
  <a href="#" class="menu-item">Контакти</a>
</nav>
```

```css
.menu-item {
  position: relative;
  text-decoration: none;
  color: #333;
  padding-bottom: 5px;
}

.menu-item::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: #007bff;
  transition: width 0.3s ease;
}

.menu-item:hover::after {
  width: 100%;
}
```

## 4. Важливі примітки

1. Трансформації не впливають на потік документа
2. Властивість transition потрібно задавати на елемент у початковому стані
3. Не всі CSS властивості можна анімувати
4. Використовуйте апаратне прискорення для кращої продуктивності:

```css
.element {
  transform: translateZ(0);
  will-change: transform;
}
```

5. Не зловживайте анімаціями та переходами - це може погіршити користувацький досвід
