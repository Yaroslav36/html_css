# Картки з перекриттям за допомогою CSS позиціонування (Частина 2)

## 3. Галерея з перекриттям та ефектом фокусу

Цей приклад демонструє, як створити галерею з карток, що перекриваються, з ефектом фокусування при наведенні.

### HTML

```html
<div class="gallery-container">
  <div class="gallery-card">
    <img src="https://picsum.photos/id/25/500/600" alt="Зображення 1" />
    <div class="card-content">
      <h3>Заголовок 1</h3>
      <p>Короткий опис першої картки</p>
    </div>
  </div>

  <div class="gallery-card">
    <img src="https://picsum.photos/id/27/500/600" alt="Зображення 2" />
    <div class="card-content">
      <h3>Заголовок 2</h3>
      <p>Короткий опис другої картки</p>
    </div>
  </div>

  <div class="gallery-card">
    <img src="https://picsum.photos/id/28/500/600" alt="Зображення 3" />
    <div class="card-content">
      <h3>Заголовок 3</h3>
      <p>Короткий опис третьої картки</p>
    </div>
  </div>

  <div class="gallery-card">
    <img src="https://picsum.photos/id/29/500/600" alt="Зображення 4" />
    <div class="card-content">
      <h3>Заголовок 4</h3>
      <p>Короткий опис четвертої картки</p>
    </div>
  </div>

  <div class="gallery-card">
    <img src="https://picsum.photos/id/30/500/600" alt="Зображення 5" />
    <div class="card-content">
      <h3>Заголовок 5</h3>
      <p>Короткий опис п'ятої картки</p>
    </div>
  </div>
</div>
```

### CSS

```css
/* Контейнер галереї */
.gallery-container {
  display: flex;
  justify-content: center;
  padding: 50px 0;
  width: 100%;
  max-width: 1000px;
  margin: 0 auto;
}

/* Базові стилі карток */
.gallery-card {
  width: 220px;
  height: 320px;
  border-radius: 12px;
  overflow: hidden;
  position: relative;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease, z-index 0s 0.3s;
  margin-right: -120px; /* Ось це створює ефект перекриття */
  cursor: pointer;
}

/* Остання картка не повинна мати правого маргіну */
.gallery-card:last-child {
  margin-right: 0;
}

/* Зображення на всю картку */
.gallery-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

/* Контент картки (заголовок і опис) */
.card-content {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 20px;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  color: white;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.card-content h3 {
  margin: 0 0 10px 0;
  font-size: 18px;
}

.card-content p {
  margin: 0;
  font-size: 14px;
  opacity: 0.8;
}

/* Ефекти при наведенні */
.gallery-card:hover {
  transform: translateY(-20px) scale(1.1);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
  z-index: 10; /* Вища картка над всіма іншими */
  transition: transform 0.3s ease, box-shadow 0.3s ease, z-index 0s;
}

.gallery-card:hover img {
  transform: scale(1.1);
}

.gallery-card:hover .card-content {
  transform: translateY(0);
}
```

### Ключові аспекти позиціонування

1. **Ефект перекриття з від'ємним маргіном**:

   - `margin-right: -120px` зміщує картки так, щоб вони перекривалися одна з одною.

2. **Регулювання порядку накладання**:

   - Збільшення `z-index` при наведенні виносить картку вперед, на передній план.
   - Затримка зміни z-index при зворотному переході (`z-index 0s 0.3s`) запобігає раптовим стрибкам під час анімації.

3. **Абсолютне позиціонування вмісту**:

   - `.card-content { position: absolute; bottom: 0; left: 0; right: 0; }` розташовує контентну частину внизу картки.

4. **Трансформація для анімації**:
   - Початкове приховування контенту з `transform: translateY(100%)` та його анімація при наведенні.
   - Ефект спливання картки з `transform: translateY(-20px) scale(1.1)` при наведенні.

## 4. Стек карток з 3D-ефектом

Цей приклад створює стек карток з 3D-ефектом при взаємодії.

### HTML

```html
<div class="stack-container">
  <div class="stack-card">
    <div class="card-face">1</div>
  </div>
  <div class="stack-card">
    <div class="card-face">2</div>
  </div>
  <div class="stack-card">
    <div class="card-face">3</div>
  </div>
  <div class="stack-card">
    <div class="card-face">4</div>
  </div>
  <div class="stack-card">
    <div class="card-face">5</div>
  </div>
</div>
```

### CSS

```css
/* Контейнер для стеку */
.stack-container {
  position: relative;
  width: 250px;
  height: 350px;
  margin: 100px auto;
  perspective: 1000px; /* Додає 3D-перспективу */
}

/* Базові стилі карток */
.stack-card {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: transform 0.5s ease, top 0.5s ease, left 0.5s ease;
  cursor: pointer;
}

/* Лицьова сторона картки */
.card-face {
  position: relative;
  width: 100%;
  height: 100%;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 40px;
  font-weight: bold;
  backface-visibility: hidden;
}

/* Ефект каскадного стека з початковими позиціями */
.stack-card:nth-child(1) {
  transform: translateZ(0px);
  background-color: #ffcdd2;
  z-index: 5;
}

.stack-card:nth-child(2) {
  top: 10px;
  left: 10px;
  transform: translateZ(-10px);
  background-color: #f8bbd0;
  z-index: 4;
}

.stack-card:nth-child(3) {
  top: 20px;
  left: 20px;
  transform: translateZ(-20px);
  background-color: #e1bee7;
  z-index: 3;
}

.stack-card:nth-child(4) {
  top: 30px;
  left: 30px;
  transform: translateZ(-30px);
  background-color: #bbdefb;
  z-index: 2;
}

.stack-card:nth-child(5) {
  top: 40px;
  left: 40px;
  transform: translateZ(-40px);
  background-color: #b2dfdb;
  z-index: 1;
}

/* Ефекти при наведенні */
.stack-card:hover {
  transform: translateZ(50px) rotateX(10deg) rotateY(10deg);
  z-index: 10;
}
```

### JavaScript для інтерактивності

```javascript
const stackCards = document.querySelectorAll(".stack-card");

// Додаємо обробник кліку на кожну картку
stackCards.forEach((card, index) => {
  // Початковий індекс для z-index
  let zIndex = 5 - index;

  card.addEventListener("click", () => {
    // Змінюємо порядок елементів у стеку
    if (zIndex !== 5) {
      // Оновлюємо z-index для всіх карток
      stackCards.forEach((c, i) => {
        let currentZ = parseInt(getComputedStyle(c).zIndex);
        if (currentZ > zIndex) {
          c.style.zIndex = currentZ - 1;
        }
      });

      // Виносимо поточну картку на верх стеку
      card.style.zIndex = 5;
      zIndex = 5;

      // Перетягуємо картку вгору в стеку
      card.style.top = "0";
      card.style.left = "0";
      card.style.transform = "translateZ(0px)";
    }
  });
});
```

### Ключові аспекти позиціонування

1. **3D-позиціонування**:

   - `perspective: 1000px` на контейнері створює 3D-перспективу.
   - `transform-style: preserve-3d` на картках зберігає 3D-ефект для дочірніх елементів.

2. **Покрокове зміщення**:

   - Кожна наступна картка зміщується на 10px вниз і вправо (`top: 10px; left: 10px`).
   - Кожна наступна картка відсувається на 10px далі в глибину з `translateZ(-10px)`.

3. **Керування порядком накладання**:
   - Спадаючі значення `z-index` забезпечують правильне накладання карток.
