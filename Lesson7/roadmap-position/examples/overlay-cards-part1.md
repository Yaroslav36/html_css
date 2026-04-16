# Картки з перекриттям за допомогою CSS позиціонування (Частина 1)

Картки з перекриттям - це поширений візуальний прийом, який використовується в сучасних веб-дизайнах для створення глибини, ієрархії та візуального інтересу. Вони чудово демонструють можливості різних методів CSS позиціонування.

## 1. Базове перекриття карток

Найпростіший спосіб створити ефект перекриття карток - використовувати `position: relative` та властивості відступів.

### HTML

```html
<div class="basic-overlap-container">
  <div class="card card-1">Картка 1</div>
  <div class="card card-2">Картка 2</div>
  <div class="card card-3">Картка 3</div>
  <div class="card card-4">Картка 4</div>
</div>
```

### CSS

```css
/* Базові стилі */
.basic-overlap-container {
  padding: 50px;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}

.card {
  width: 200px;
  height: 120px;
  padding: 20px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  font-size: 18px;
  position: relative;
}

/* Горизонтальне перекриття (по осі X) */
.card-1 {
  background-color: #f8d7da;
  z-index: 4;
}

.card-2 {
  background-color: #d4edda;
  margin-top: -80px;
  margin-left: 40px;
  z-index: 3;
}

.card-3 {
  background-color: #cce5ff;
  margin-top: -80px;
  margin-left: 80px;
  z-index: 2;
}

.card-4 {
  background-color: #fff3cd;
  margin-top: -80px;
  margin-left: 120px;
  z-index: 1;
}
```

### Ключові аспекти позиціонування

1. **Відносне позиціонування карток**:
   - `position: relative` застосовується до кожної картки для створення нового контексту накладання.

2. **Контроль порядку накладання**:
   - Властивість `z-index` визначає, які картки будуть відображатися над іншими.
   - Більші значення z-index розміщують елементи над елементами з меншими значеннями.

3. **Зміщення за допомогою margins**:
   - Від'ємні верхні маргіни (`margin-top: -80px`) створюють вертикальне перекриття.
   - Позитивні ліві маргіни (`margin-left: 40px`) створюють каскадний ефект горизонтального зміщення.

## 2. Віялоподібне розташування карток

Цей ефект дозволяє розташувати картки у вигляді віяла.

### HTML

```html
<div class="fan-container">
  <div class="fan-card fan-card-1">1</div>
  <div class="fan-card fan-card-2">2</div>
  <div class="fan-card fan-card-3">3</div>
  <div class="fan-card fan-card-4">4</div>
  <div class="fan-card fan-card-5">5</div>
</div>
```

### CSS

```css
/* Контейнер для віялоподібних карток */
.fan-container {
  position: relative;
  width: 300px;
  height: 300px;
  margin: 100px auto;
}

/* Базові стилі карток */
.fan-card {
  position: absolute;
  width: 150px;
  height: 200px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  font-weight: bold;
  transition: transform 0.3s ease;
  transform-origin: bottom center;
  /* Початкова позиція - по центру внизу контейнера */
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}

/* Різні кольори для карток */
.fan-card-1 { background-color: #ffcccb; z-index: 5; }
.fan-card-2 { background-color: #ffdab9; z-index: 4; }
.fan-card-3 { background-color: #ffffcc; z-index: 3; }
.fan-card-4 { background-color: #e0ffff; z-index: 2; }
.fan-card-5 { background-color: #d8bfd8; z-index: 1; }

/* Застосовуємо поворот для створення віяла */
.fan-container:hover .fan-card-1 { transform: translateX(-50%) rotate(-25deg); }
.fan-container:hover .fan-card-2 { transform: translateX(-50%) rotate(-12.5deg); }
.fan-container:hover .fan-card-3 { transform: translateX(-50%) rotate(0deg); }
.fan-container:hover .fan-card-4 { transform: translateX(-50%) rotate(12.5deg); }
.fan-container:hover .fan-card-5 { transform: translateX(-50%) rotate(25deg); }
```

### Ключові аспекти позиціонування

1. **Абсолютне позиціонування всередині контейнера**:
   - Контейнер має `position: relative` для створення контексту позиціонування.
   - Всі картки мають `position: absolute; bottom: 0; left: 50%;` для розміщення внизу по центру.

2. **Центрування з transform**:
   - `transform: translateX(-50%)` центрує картки, компенсуючи їх власну ширину.

3. **Трансформація для ефекту віяла**:
   - `transform-origin: bottom center` встановлює точку, навколо якої відбувається обертання.
   - При наведенні додаються різні кути обертання для розкриття віяла.

4. **Плавний перехід**:
   - `transition: transform 0.3s ease` додає анімацію для плавного розкриття віяла при наведенні.
