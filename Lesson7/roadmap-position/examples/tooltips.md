# Спливаючі підказки з використанням CSS позиціонування

Спливаючі підказки (tooltips) — це невеликі інформаційні блоки, що з'являються при наведенні або кліку на елемент. Вони ідеально демонструють використання абсолютного позиціонування у поєднанні з псевдоелементами.

## 1. Базові підказки з використанням атрибута title

Найпростіший спосіб створити підказку — використати HTML-атрибут `title`:

```html
<button title="Це підказка для кнопки">Наведіть курсор</button>
```

Однак такі підказки мають обмежені можливості стилізації. Розглянемо більш гнучкі варіанти з CSS.

## 2. Базові CSS підказки з псевдоелементами

### HTML

```html
<div class="tooltip-container">
  <button class="tooltip-trigger">Наведіть курсор</button>
  <span class="tooltip-text">Це базова CSS підказка</span>
</div>
```

### CSS

```css
/* Контейнер підказки */
.tooltip-container {
  position: relative;
  display: inline-block;
}

/* Текст підказки */
.tooltip-text {
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background-color: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s, visibility 0.3s;
  z-index: 100;
  margin-bottom: 5px;
}

/* Трикутник (стрілка) підказки */
.tooltip-text::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-width: 5px;
  border-style: solid;
  border-color: #333 transparent transparent transparent;
}

/* Показ підказки при наведенні */
.tooltip-container:hover .tooltip-text {
  opacity: 1;
  visibility: visible;
}
```

### Ключові аспекти позиціонування

1. **Відносне позиціонування контейнера**:
   - `.tooltip-container { position: relative; }` створює контекст позиціонування для підказки.

2. **Абсолютне позиціонування підказки**:
   - `.tooltip-text { position: absolute; bottom: 100%; left: 50%; }` розміщує підказку над елементом, центруючи її.
   - `transform: translateX(-50%);` забезпечує точне центрування відносно батьківського елемента.

3. **Створення стрілки з псевдоелемента**:
   - `.tooltip-text::after { position: absolute; top: 100%; left: 50%; }` позиціонує стрілку внизу підказки.
   - Комбінація властивостей `border` створює трикутник, який вказує на елемент.

## 3. Різні позиції підказок

### HTML

```html
<div class="container">
  <div class="tooltip-container">
    <button class="tooltip-trigger">Зверху</button>
    <span class="tooltip-text tooltip-top">Підказка зверху</span>
  </div>
  
  <div class="tooltip-container">
    <button class="tooltip-trigger">Справа</button>
    <span class="tooltip-text tooltip-right">Підказка справа</span>
  </div>
  
  <div class="tooltip-container">
    <button class="tooltip-trigger">Знизу</button>
    <span class="tooltip-text tooltip-bottom">Підказка знизу</span>
  </div>
  
  <div class="tooltip-container">
    <button class="tooltip-trigger">Зліва</button>
    <span class="tooltip-text tooltip-left">Підказка зліва</span>
  </div>
</div>
```

### CSS

```css
/* Базові стилі */
.container {
  display: flex;
  justify-content: space-around;
  margin: 100px 0;
}

.tooltip-container {
  position: relative;
  display: inline-block;
}

.tooltip-trigger {
  padding: 10px 15px;
  background-color: #f1f1f1;
  border: 1px solid #ddd;
  border-radius: 4px;
  cursor: pointer;
}

/* Базові стилі підказки */
.tooltip-text {
  position: absolute;
  background-color: #333;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s, visibility 0.3s;
  z-index: 100;
}

/* Стрілка підказки (базові стилі) */
.tooltip-text::after {
  content: "";
  position: absolute;
  border-width: 5px;
  border-style: solid;
}

/* Підказка зверху */
.tooltip-top {
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  margin-bottom: 10px;
}

.tooltip-top::after {
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-color: #333 transparent transparent transparent;
}

/* Підказка справа */
.tooltip-right {
  top: 50%;
  left: 100%;
  transform: translateY(-50%);
  margin-left: 10px;
}

.tooltip-right::after {
  top: 50%;
  right: 100%;
  transform: translateY(-50%);
  border-color: transparent #333 transparent transparent;
}

/* Підказка знизу */
.tooltip-bottom {
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  margin-top: 10px;
}

.tooltip-bottom::after {
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-color: transparent transparent #333 transparent;
}

/* Підказка зліва */
.tooltip-left {
  top: 50%;
  right: 100%;
  transform: translateY(-50%);
  margin-right: 10px;
}

.tooltip-left::after {
  top: 50%;
  left: 100%;
  transform: translateY(-50%);
  border-color: transparent transparent transparent #333;
}

/* Показ підказки при наведенні */
.tooltip-container:hover .tooltip-text {
  opacity: 1;
  visibility: visible;
}
```

## 4. Розширені підказки з контентом

### HTML

```html
<div class="enhanced-tooltip-container">
  <div class="product-card">
    <img src="product-image.jpg" alt="Продукт">
    <h3>Назва продукту</h3>
    <p class="price">$99.99</p>
    <button class="info-button" aria-label="Додаткова інформація">i</button>
  </div>
  
  <div class="enhanced-tooltip">
    <h4>Детальна інформація</h4>
    <div class="tooltip-content">
      <p><strong>Характеристики:</strong></p>
      <ul>
        <li>Особливість 1</li>
        <li>Особливість 2</li>
        <li>Особливість 3</li>
      </ul>
      <p><strong>Гарантія:</strong> 12 місяців</p>
      <a href="#" class="tooltip-link">Детальніше</a>
    </div>
    <span class="tooltip-close" aria-label="Закрити підказку">&times;</span>
  </div>
</div>
```

### CSS

```css
/* Базові стилі */
.enhanced-tooltip-container {
  position: relative;
  display: inline-block;
}

.product-card {
  width: 250px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  text-align: center;
  position: relative;
}

.product-card img {
  max-width: 100%;
  height: auto;
  margin-bottom: 15px;
}

.info-button {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  background-color: #3498db;
  color: white;
  border: none;
  font-style: italic;
  font-weight: bold;
  cursor: pointer;
}

/* Розширена підказка */
.enhanced-tooltip {
  position: absolute;
  top: 50%;
  left: 100%;
  transform: translateY(-50%);
  margin-left: 15px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
  width: 300px;
  padding: 20px;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s, visibility 0.3s;
  z-index: 100;
}

/* Стрілка підказки */
.enhanced-tooltip::before {
  content: "";
  position: absolute;
  top: 50%;
  right: 100%;
  transform: translateY(-50%);
  border-width: 10px;
  border-style: solid;
  border-color: transparent white transparent transparent;
}

/* Заголовок підказки */
.enhanced-tooltip h4 {
  margin-top: 0;
  color: #333;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 15px;
}

/* Вміст підказки */
.tooltip-content {
  font-size: 14px;
  line-height: 1.6;
}

.tooltip-content ul {
  padding-left: 20px;
  margin: 10px 0;
}

.tooltip-link {
  display: inline-block;
  margin-top: 10px;
  color: #3498db;
  text-decoration: none;
}

.tooltip-link:hover {
  text-decoration: underline;
}

/* Кнопка закриття */
.tooltip-close {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 20px;
  color: #999;
  cursor: pointer;
}

.tooltip-close:hover {
  color: #333;
}

/* Активація підказки */
.info-button:focus + .enhanced-tooltip,
.info-button:hover + .enhanced-tooltip,
.enhanced-tooltip:hover {
  opacity: 1;
  visibility: visible;
}
```

### JavaScript для клікабельної підказки

```javascript
const infoButton = document.querySelector('.info-button');
const enhancedTooltip = document.querySelector('.enhanced-tooltip');
const tooltipClose = document.querySelector('.tooltip-close');

// Переключення відображення підказки по кліку
infoButton.addEventListener('click', (e) => {
  e.stopPropagation();
  enhancedTooltip.classList.toggle('visible');
});

// Закриття підказки при кліку на кнопку закриття
tooltipClose.addEventListener('click', () => {
  enhancedTooltip.classList.remove('visible');
});

// Закриття підказки при кліку поза нею
document.addEventListener('click', (e) => {
  if (!enhancedTooltip.contains(e.target) && e.target !== infoButton) {
    enhancedTooltip.classList.remove('visible');
  }
});

// Додатковий CSS для JS-активації
const additionalCSS = `
.enhanced-tooltip.visible {
  opacity: 1;
  visibility: visible;
}
`;

// Додавання CSS до сторінки
const style = document.createElement('style');
style.textContent = additionalCSS;
document.head.appendChild(style);
```

## 5. Підказки, що слідують за курсором

### HTML

```html
<div class="cursor-tooltip-container">
  <div class="hover-area">
    Рухайте курсор в цій області для підказки, що слідує за курсором
  </div>
  <div class="cursor-tooltip">Я слідую за вашим курсором!</div>
</div>
```

### CSS

```css
.cursor-tooltip-container {
  position: relative;
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.hover-area {
  height: 200px;
  background-color: #f9f9f9;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  border: 1px dashed #ddd;
  border-radius: 8px;
  text-align: center;
  color: #777;
}

.cursor-tooltip {
  position: fixed; /* Позиціонування відносно вікна перегляду */
  background-color: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 14px;
  pointer-events: none; /* Важливо! Це дозволяє підказці не блокувати ваші миші події */
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s;
  z-index: 1000;
}
```

### JavaScript

```javascript
const hoverArea = document.querySelector('.hover-area');
const cursorTooltip = document.querySelector('.cursor-tooltip');

// Показувати підказку при вході курсора в область
hoverArea.addEventListener('mouseenter', () => {
  cursorTooltip.style.opacity = '1';
  cursorTooltip.style.visibility = 'visible';
});

// Приховувати підказку при виході курсора з області
hoverArea.addEventListener('mouseleave', () => {
  cursorTooltip.style.opacity = '0';
  cursorTooltip.style.visibility = 'hidden';
});

// Оновлювати позицію підказки при русі курсора
hoverArea.addEventListener('mousemove', (e) => {
  // Зміщення від курсора
  const offsetX = 15;
  const offsetY = 15;
  
  // Розміри підказки
  const tooltipWidth = cursorTooltip.offsetWidth;
  const tooltipHeight = cursorTooltip.offsetHeight;
  
  // Розміри вікна перегляду
  const viewportWidth = window.innerWidth;
  const viewportHeight = window.innerHeight;
  
  // Базова позиція (зміщення від курсора)
  let posX = e.clientX + offsetX;
  let posY = e.clientY + offsetY;
  
  // Перевірка, чи не виходить підказка за межі вікна справа
  if (posX + tooltipWidth > viewportWidth) {
    posX = e.clientX - offsetX - tooltipWidth;
  }
  
  // Перевірка, чи не виходить підказка за межі вікна знизу
  if (posY + tooltipHeight > viewportHeight) {
    posY = e.clientY - offsetY - tooltipHeight;
  }
  
  // Застосування позиції
  cursorTooltip.style.left = `${posX}px`;
  cursorTooltip.style.top = `${posY}px`;
});
```

## Особливості доступності для підказок

Для забезпечення доступності ваших підказок, дотримуйтесь цих рекомендацій:

```html
<div class="tooltip-container">
  <button class="tooltip-trigger" 
          aria-describedby="tooltip-1">Кнопка з підказкою</button>
  <span class="tooltip-text" 
         id="tooltip-1" 
         role="tooltip">Це доступна підказка</span>
</div>
```

```css
/* Додайте підтримку клавіатурного фокусу */
.tooltip-container:focus-within .tooltip-text {
  opacity: 1;
  visibility: visible;
}
```

## Ключові принципи позиціонування підказок

1. **Створення контексту позиціонування**:
   - Використання `position: relative` на батьківському елементі створює контекст для розміщення підказки.

2. **Розміщення підказки**:
   - `position: absolute` для стандартних підказок, прив'язаних до елемента.
   - `position: fixed` для підказок, що слідують за курсором.

3. **Центрування та вирівнювання**:
   - Використання комбінації `left: 50%` або `top: 50%` з `transform: translateX(-50%)` або `transform: translateY(-50%)` для точного центрування.

4. **Відстань від тригера**:
   - Використання `margin` для створення відступу між підказкою та її тригером.

5. **Створення стрілок**:
   - Використання псевдоелементів та CSS-трикутників через `border` для створення стрілок.

6. **Видимість та анімація**:
   - Використання `opacity` та `visibility` з `transition` для плавної появи та зникнення.

7. **Адаптивність позиціонування**:
   - Врахування меж вікна перегляду для підказок, що можуть виходити за межі екрана.

## Висновок

Спливаючі підказки демонструють потужність абсолютного та фіксованого позиціонування у поєднанні з псевдоелементами. Вони дозволяють створювати інтерактивні елементи інтерфейсу, які покращують досвід користувача, надаючи додаткову інформацію, коли це необхідно, без перевантаження основного інтерфейсу.
