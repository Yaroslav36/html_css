# Створення модальних вікон з CSS позиціонуванням

Модальні вікна - це один з найпоширеніших компонентів інтерфейсу, що використовують позиціонування. Вони відображають вміст поверх основної сторінки і зазвичай вимагають взаємодії користувача перед продовженням роботи з основною сторінкою.

## Базовий модальний діалог

### HTML

```html
<button class="modal-open-btn">Відкрити модальне вікно</button>

<div class="modal-overlay">
  <div class="modal">
    <button class="modal-close-btn">&times;</button>
    <h2>Модальне вікно</h2>
    <p>Це приклад модального вікна, створеного за допомогою CSS позиціонування.</p>
    <p>Клацніть на кнопку "закрити" або за межами вікна, щоб закрити модальне вікно.</p>
    <button class="modal-action-btn">Підтвердити</button>
  </div>
</div>
```

### CSS

```css
/* Базові стилі */
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
}

/* Кнопка для відкриття модального вікна */
.modal-open-btn {
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.modal-open-btn:hover {
  background-color: #2980b9;
}

/* Оверлей модального вікна */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s ease;
}

.modal-overlay.active {
  opacity: 1;
  visibility: visible;
}

/* Модальне вікно */
.modal {
  position: relative;
  background-color: white;
  padding: 30px;
  border-radius: 8px;
  max-width: 500px;
  width: 90%;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  transform: translateY(-20px);
  transition: transform 0.3s ease;
}

.modal-overlay.active .modal {
  transform: translateY(0);
}

/* Кнопка закриття */
.modal-close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: #777;
  padding: 0;
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
}

.modal-close-btn:hover {
  background-color: #f1f1f1;
  color: #333;
}

/* Кнопка дії */
.modal-action-btn {
  padding: 10px 20px;
  background-color: #27ae60;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 15px;
}

.modal-action-btn:hover {
  background-color: #219653;
}
```

### JavaScript

```javascript
// Вибір елементів
const openModalBtn = document.querySelector('.modal-open-btn');
const closeModalBtn = document.querySelector('.modal-close-btn');
const modalOverlay = document.querySelector('.modal-overlay');
const modal = document.querySelector('.modal');

// Відкриття модального вікна
openModalBtn.addEventListener('click', () => {
  modalOverlay.classList.add('active');
});

// Закриття модального вікна при кліку на кнопку закриття
closeModalBtn.addEventListener('click', () => {
  modalOverlay.classList.remove('active');
});

// Закриття модального вікна при кліку на оверлей (за межами модального вікна)
modalOverlay.addEventListener('click', (event) => {
  if (event.target === modalOverlay) {
    modalOverlay.classList.remove('active');
  }
});

// Закриття модального вікна при натисканні клавіші Escape
document.addEventListener('keydown', (event) => {
  if (event.key === 'Escape' && modalOverlay.classList.contains('active')) {
    modalOverlay.classList.remove('active');
  }
});
```

## Ключові аспекти CSS позиціонування у модальних вікнах

1. **Оверлей використовує `position: fixed`**:
   - Це забезпечує, що оверлей покриває весь екран незалежно від прокрутки.
   - Властивості `top: 0; left: 0; right: 0; bottom: 0;` розтягують оверлей на весь екран.

2. **Центрування модального вікна всередині оверлею**:
   - Використання Flexbox (`display: flex; justify-content: center; align-items: center;`) забезпечує просте центрування вікна.
   - Це сучасний підхід, що замінює старий метод з абсолютним позиціонуванням і негативними margin.

3. **Модальне вікно використовує `position: relative`**:
   - Це створює контекст позиціонування для елементів всередині модального вікна.
   - Дозволяє абсолютно позиціонувати кнопку закриття.

4. **Кнопка закриття позиціонована абсолютно**:
   - `position: absolute; top: 10px; right: 10px;` розміщує кнопку у верхньому правому куті модального вікна.

5. **Використання z-index для шарів**:
   - Оверлей має високий `z-index: 1000`, щоб бути над усіма іншими елементами сторінки.

## Варіанти і модифікації

### 1. Модальне вікно, що відкривається збоку

```css
.modal-overlay.active .modal {
  transform: translateX(0);
}

/* Варіант: модальне вікно справа */
.modal {
  transform: translateX(100%);
  position: fixed;
  top: 0;
  right: 0;
  height: 100%;
  border-radius: 0;
  max-width: 400px;
}

/* Варіант: модальне вікно зліва */
.modal {
  transform: translateX(-100%);
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  border-radius: 0;
  max-width: 400px;
}
```

### 2. Модальне вікно, що відкривається знизу (шухляда)

```css
.modal-overlay.active .modal {
  transform: translateY(0);
}

.modal {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  transform: translateY(100%);
  max-width: 100%;
  border-radius: 20px 20px 0 0;
}
```

### 3. Модальне вікно з вкладеними модальними вікнами

```html
<div class="modal">
  <!-- Вміст першого модального вікна -->
  <button class="nested-modal-open-btn">Відкрити вкладене модальне вікно</button>
</div>

<div class="modal-overlay nested-modal">
  <div class="modal">
    <!-- Вміст вкладеного модального вікна -->
  </div>
</div>
```

```css
.nested-modal {
  z-index: 1100; /* Більший z-index, ніж у основного модального вікна */
}
```

## Адаптивність модальних вікон

```css
/* Базові розміри для великих екранів */
.modal {
  max-width: 600px;
  padding: 40px;
}

/* Середні екрани */
@media (max-width: 768px) {
  .modal {
    max-width: 90%;
    padding: 30px;
  }
}

/* Мобільні пристрої */
@media (max-width: 480px) {
  .modal {
    max-width: 100%;
    width: 100%;
    margin: 0;
    border-radius: 0;
    padding: 20px;
  }
  
  /* Для мобільних пристроїв модальне вікно може займати весь екран */
  .modal-overlay {
    align-items: flex-start;
  }
  
  .modal-overlay.active .modal {
    height: 100%;
  }
}
```

## Доступність модальних вікон

Для забезпечення доступності модальних вікон, додайте ці атрибути:

```html
<div 
  class="modal-overlay" 
  role="dialog" 
  aria-modal="true" 
  aria-labelledby="modalTitle" 
  aria-describedby="modalDescription">
  <div class="modal">
    <button 
      class="modal-close-btn" 
      aria-label="Закрити модальне вікно">&times;</button>
    <h2 id="modalTitle">Модальне вікно</h2>
    <p id="modalDescription">Це приклад модального вікна...</p>
    <!-- Вміст модального вікна -->
  </div>
</div>
```

JavaScript для доступності:

```javascript
// Фокусування на модальному вікні при відкритті
openModalBtn.addEventListener('click', () => {
  modalOverlay.classList.add('active');
  
  // Зберігаємо елемент, що мав фокус до відкриття модального вікна
  const lastFocus = document.activeElement;
  
  // Фокус на першому фокусованому елементі в модальному вікні
  const focusableElements = modal.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
  if (focusableElements.length) {
    focusableElements[0].focus();
  }
});

// Керування фокусом у модальному вікні (захоплення фокусу)
modal.addEventListener('keydown', (event) => {
  if (event.key === 'Tab') {
    const focusableElements = modal.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];
    
    // Цикл фокусу при натисканні Tab
    if (event.shiftKey && document.activeElement === firstElement) {
      event.preventDefault();
      lastElement.focus();
    } else if (!event.shiftKey && document.activeElement === lastElement) {
      event.preventDefault();
      firstElement.focus();
    }
  }
});
```

## Висновок

Модальні вікна є прекрасним прикладом, як різні типи CSS позиціонування працюють разом для створення інтерактивних компонентів інтерфейсу:

- `position: fixed` використовується для фіксації оверлею на екрані
- `position: relative` створює контекст позиціонування для дочірніх елементів модального вікна
- `position: absolute` дозволяє точно розміщувати елементи керування всередині модального вікна

Поєднавши ці техніки позиціонування з сучасними підходами (Flexbox для центрування, CSS-переходи для анімацій), ви можете створювати високоякісні, доступні та адаптивні модальні вікна для ваших проєктів.
