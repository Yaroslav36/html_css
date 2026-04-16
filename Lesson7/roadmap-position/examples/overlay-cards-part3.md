# Картки з перекриттям за допомогою CSS позиціонування (Частина 3)

## 5. Карусель з перекриттям

Цей приклад демонструє, як створити каруселі з карток, що перекриваються.

### HTML

```html
<div class="carousel-container">
  <div class="carousel-track">
    <div class="carousel-card">
      <img src="image1.jpg" alt="Зображення 1">
      <div class="card-caption">Елемент 1</div>
    </div>
    <div class="carousel-card">
      <img src="image2.jpg" alt="Зображення 2">
      <div class="card-caption">Елемент 2</div>
    </div>
    <div class="carousel-card">
      <img src="image3.jpg" alt="Зображення 3">
      <div class="card-caption">Елемент 3</div>
    </div>
    <div class="carousel-card">
      <img src="image4.jpg" alt="Зображення 4">
      <div class="card-caption">Елемент 4</div>
    </div>
    <div class="carousel-card">
      <img src="image5.jpg" alt="Зображення 5">
      <div class="card-caption">Елемент 5</div>
    </div>
  </div>
  
  <div class="carousel-nav">
    <button class="prev-btn">←</button>
    <button class="next-btn">→</button>
  </div>
</div>
```

### CSS

```css
/* Контейнер каруселі */
.carousel-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 50px auto;
  padding: 20px 0;
  overflow: hidden;
}

/* Трек каруселі - контейнер для карток */
.carousel-track {
  display: flex;
  transition: transform 0.5s ease;
}

/* Картки каруселі */
.carousel-card {
  min-width: 250px;
  height: 350px;
  border-radius: 10px;
  overflow: hidden;
  position: relative;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  margin-right: -50px; /* Створює ефект перекриття */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

/* Зображення в карусельній картці */
.carousel-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Підпис до картки */
.card-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 15px;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  font-size: 16px;
  text-align: center;
}

/* Кнопки навігації */
.carousel-nav {
  display: flex;
  justify-content: space-between;
  position: absolute;
  width: calc(100% - 40px);
  top: 50%;
  left: 20px;
  transform: translateY(-50%);
}

.prev-btn, .next-btn {
  background-color: rgba(255, 255, 255, 0.7);
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 18px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  z-index: 10;
  transition: background-color 0.3s;
}

.prev-btn:hover, .next-btn:hover {
  background-color: rgba(255, 255, 255, 0.9);
}

/* Активна картка */
.carousel-card.active {
  transform: scale(1.05);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
  z-index: 5;
}
```

### JavaScript

```javascript
const track = document.querySelector('.carousel-track');
const cards = document.querySelectorAll('.carousel-card');
const prevBtn = document.querySelector('.prev-btn');
const nextBtn = document.querySelector('.next-btn');

let currentIndex = 0;
const cardWidth = cards[0].offsetWidth - 50; // Враховуємо перекриття

// Ініціалізація каруселі
function initCarousel() {
  // Встановлюємо першу картку як активну
  cards[0].classList.add('active');
}

// Переміщення до певної картки
function moveToCard(index) {
  if (index < 0) index = 0;
  if (index >= cards.length) index = cards.length - 1;
  
  currentIndex = index;
  
  // Оновлюємо активну картку
  cards.forEach(card => card.classList.remove('active'));
  cards[currentIndex].classList.add('active');
  
  // Зміщуємо трек до поточної картки
  track.style.transform = `translateX(-${currentIndex * cardWidth}px)`;
}

// Обробники подій для кнопок
prevBtn.addEventListener('click', () => {
  moveToCard(currentIndex - 1);
});

nextBtn.addEventListener('click', () => {
  moveToCard(currentIndex + 1);
});

// Ініціалізуємо карусель при завантаженні
initCarousel();
```

### Ключові аспекти позиціонування

1. **Перекриття за допомогою від'ємних маргінів**:
   - `margin-right: -50px` для карток створює ефект перекриття.

2. **Абсолютне позиціонування для навігації та підписів**:
   - Кнопки навігації позиціонуються абсолютно відносно контейнера каруселі.
   - Підписи карток позиціонуються абсолютно відносно самих карток.

3. **Керування елементами через z-index**:
   - Активна картка має підвищений `z-index` для відображення над іншими.
   - Кнопки навігації мають високий `z-index`, щоб бути завжди зверху.

## 6. Картки профілів з перекриттям елементів

У цьому прикладі ми створимо картки профілів, де фотографія перекриває межу картки.

### HTML

```html
<div class="profile-cards-container">
  <div class="profile-card">
    <div class="profile-image-wrapper">
      <img src="profile1.jpg" alt="Профіль 1" class="profile-image">
    </div>
    <div class="profile-content">
      <h3 class="profile-name">Анна Ковальчук</h3>
      <p class="profile-title">Веб-розробник</p>
      <p class="profile-description">Спеціаліст з фронтенд-розробки з 5-річним досвідом роботи в індустрії.</p>
      <div class="profile-social">
        <a href="#" class="social-icon">FB</a>
        <a href="#" class="social-icon">TW</a>
        <a href="#" class="social-icon">IN</a>
      </div>
    </div>
  </div>
  
  <div class="profile-card">
    <div class="profile-image-wrapper">
      <img src="profile2.jpg" alt="Профіль 2" class="profile-image">
    </div>
    <div class="profile-content">
      <h3 class="profile-name">Іван Петренко</h3>
      <p class="profile-title">UI/UX Дизайнер</p>
      <p class="profile-description">Творчий дизайнер з досвідом роботи над проєктами для провідних компаній.</p>
      <div class="profile-social">
        <a href="#" class="social-icon">FB</a>
        <a href="#" class="social-icon">TW</a>
        <a href="#" class="social-icon">IN</a>
      </div>
    </div>
  </div>
  
  <div class="profile-card">
    <div class="profile-image-wrapper">
      <img src="profile3.jpg" alt="Профіль 3" class="profile-image">
    </div>
    <div class="profile-content">
      <h3 class="profile-name">Олена Сидоренко</h3>
      <p class="profile-title">Менеджер проєктів</p>
      <p class="profile-description">Досвідчений менеджер з успішною історією розробки та запуску продуктів.</p>
      <div class="profile-social">
        <a href="#" class="social-icon">FB</a>
        <a href="#" class="social-icon">TW</a>
        <a href="#" class="social-icon">IN</a>
      </div>
    </div>
  </div>
</div>
```

### CSS

```css
/* Контейнер карток профілів */
.profile-cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 30px;
  padding: 40px 20px;
  max-width: 1200px;
  margin: 0 auto;
}

/* Картка профілю */
.profile-card {
  width: 300px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  overflow: visible;
  position: relative;
  padding-top: 80px; /* Місце для фото, що виступає за межі */
}

/* Обгортка для зображення профілю */
.profile-image-wrapper {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  overflow: hidden;
  position: absolute;
  top: -60px; /* Половина висоти виходить за верхню межу картки */
  left: 50%;
  transform: translateX(-50%);
  border: 5px solid white;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

/* Зображення профілю */
.profile-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Вміст профілю */
.profile-content {
  padding: 20px;
  text-align: center;
}

.profile-name {
  margin: 0 0 5px 0;
  font-size: 22px;
  color: #333;
}

.profile-title {
  margin: 0 0 15px 0;
  font-size: 16px;
  color: #666;
  font-style: italic;
}

.profile-description {
  margin: 0 0 20px 0;
  font-size: 14px;
  color: #777;
  line-height: 1.6;
}

/* Соціальні іконки */
.profile-social {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.social-icon {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background-color: #f1f1f1;
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
  color: #333;
  font-size: 14px;
  font-weight: bold;
  transition: background-color 0.3s;
}

.social-icon:hover {
  background-color: #e0e0e0;
}

/* Ефекти при наведенні */
.profile-card:hover {
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  transform: translateY(-5px);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.profile-card:hover .profile-image-wrapper {
  transform: translateX(-50%) scale(1.05);
  transition: transform 0.3s ease;
}
```

### Ключові аспекти позиціонування

1. **Абсолютне позиціонування для фотографії профілю**:
   - `.profile-image-wrapper { position: absolute; top: -60px; }` розміщує фотографію так, щоб вона виступала за верхню межу картки.
   - `left: 50%; transform: translateX(-50%);` центрує фотографію горизонтально.

2. **Відносне позиціонування для картки**:
   - `.profile-card { position: relative; }` створює контекст позиціонування для абсолютно позиціонованої фотографії.
   - `padding-top: 80px;` створює простір у верхній частині картки для фотографії, що перекриває межу.

3. **Накладання елементів**:
   - `overflow: visible;` на картці дозволяє фотографії виходити за її межі.
   - `border: 5px solid white;` на обгортці зображення створює ефект рамки, що перекриває картку.

## Ключові принципи створення карток з перекриттям

1. **Використання різних типів позиціонування**:
   - `position: relative` для створення контексту позиціонування
   - `position: absolute` для точного розміщення елементів
   - Комбінування позиціонування з трансформаціями для досягнення складних ефектів

2. **Контроль порядку накладання**:
   - Використання `z-index` для визначення, які елементи відображаються зверху
   - Керування порядком накладання при інтерактивних діях (наведенні, кліках)

3. **Методи перекриття**:
   - Від'ємні маргіни (`margin-right: -50px`)
   - Абсолютне позиціонування з виходом за межі батьківського елемента
   - Використання трансформацій для зміщення (`transform: translateX(-50%)`)

4. **Створення глибини та 3D-ефектів**:
   - Використання `perspective` для 3D-простору
   - `transform-style: preserve-3d` для збереження 3D-ефектів
   - `translateZ()` для переміщення елементів у 3D-просторі

5. **Анімація та інтерактивність**:
   - `transition` для плавних переходів між станами
   - Зміна стилів (:hover, :focus, .active) для інтерактивних ефектів

## Висновок

Картки з перекриттям дозволяють створювати цікаві візуальні ефекти, що привертають увагу користувача та покращують досвід взаємодії з інтерфейсом. Комбінування різних методів CSS-позиціонування дозволяє досягти широкого спектру ефектів: від простого перекриття до складних 3D-карусель. Ключем до успішного впровадження таких елементів є розуміння принципів позиціонування, контролю порядку накладання та трансформацій.
