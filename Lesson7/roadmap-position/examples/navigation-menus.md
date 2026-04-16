# Навігаційні меню з використанням CSS позиціонування

Навігаційні меню - ідеальний приклад застосування різних типів позиціонування для створення зручних та ефективних інтерфейсів. Розглянемо найпопулярніші варіанти реалізації навігаційних меню.

## 1. Фіксована навігаційна панель (Fixed Navigation Bar)

### HTML структура

```html
<header class="fixed-header">
  <div class="container">
    <a href="#" class="logo">Лого сайту</a>
    <nav class="main-nav">
      <ul>
        <li><a href="#home">Головна</a></li>
        <li><a href="#about">Про нас</a></li>
        <li><a href="#services">Послуги</a></li>
        <li><a href="#portfolio">Портфоліо</a></li>
        <li><a href="#contact">Контакти</a></li>
      </ul>
    </nav>
    <button class="mobile-menu-toggle">☰</button>
  </div>
</header>

<main>
  <section id="home" class="section">
    <h1>Головна секція</h1>
    <p>Контент головної секції...</p>
  </section>
  <!-- інші секції... -->
</main>
```

### CSS для фіксованої навігації

```css
/* Базові стилі */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  padding-top: 70px; /* Компенсація висоти фіксованого заголовка */
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Фіксований заголовок */
.fixed-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #ffffff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  height: 70px;
}

/* Логотип */
.logo {
  font-size: 24px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}

/* Навігаційне меню */
.main-nav ul {
  display: flex;
  list-style: none;
}

.main-nav li {
  margin-left: 20px;
}

.main-nav a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  padding: 10px 0;
  position: relative;
  transition: color 0.3s;
}

.main-nav a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #3498db;
  transition: width 0.3s;
}

.main-nav a:hover {
  color: #3498db;
}

.main-nav a:hover::after {
  width: 100%;
}

/* Кнопка мобільного меню */
.mobile-menu-toggle {
  display: none;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
}

/* Секції контенту */
.section {
  padding: 80px 0;
  min-height: 100vh;
}

/* Медіа-запити для адаптивності */
@media (max-width: 768px) {
  .main-nav {
    display: none;
    position: absolute;
    top: 70px;
    left: 0;
    width: 100%;
    background-color: #ffffff;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }
  
  .main-nav.active {
    display: block;
  }
  
  .main-nav ul {
    flex-direction: column;
    padding: 20px;
  }
  
  .main-nav li {
    margin: 0;
    margin-bottom: 15px;
  }
  
  .mobile-menu-toggle {
    display: block;
  }
}
```

### JavaScript для мобільного меню

```javascript
const mobileMenuToggle = document.querySelector('.mobile-menu-toggle');
const mainNav = document.querySelector('.main-nav');

mobileMenuToggle.addEventListener('click', () => {
  mainNav.classList.toggle('active');
});
```

### Ключові аспекти позиціонування

1. **Фіксоване позиціонування для шапки**:
   - `position: fixed` забезпечує, що навігаційна панель завжди видима при прокрутці.
   - `top: 0; left: 0; width: 100%;` розтягує навігаційну панель на всю ширину екрана.
   - `z-index: 1000` розміщує навігаційну панель над іншими елементами сторінки.

2. **Компенсація для контенту**:
   - `body { padding-top: 70px; }` додає верхній відступ для компенсації висоти фіксованої навігаційної панелі.

3. **Позиціонування мобільного меню**:
   - На мобільних пристроях меню використовує `position: absolute` для відображення під шапкою.
   - `top: 70px; left: 0; width: 100%;` розташовує меню під шапкою на повну ширину.
