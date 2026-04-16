# Навігаційні меню з використанням CSS позиціонування (Частина 2)

## 2. "Липка" навігаційна панель (Sticky Navigation Bar)

"Липка" навігація поєднує переваги статичної та фіксованої навігації - спочатку вона поводиться як звичайний елемент, але при прокрутці до певної точки стає фіксованою.

### HTML структура

```html
<div class="pre-header">
  <div class="container">
    <div class="contact-info">
      <a href="tel:+380123456789">+38 (012) 345-67-89</a>
      <a href="mailto:info@example.com">info@example.com</a>
    </div>
    <div class="social-links">
      <a href="#" aria-label="Facebook">FB</a>
      <a href="#" aria-label="Twitter">TW</a>
      <a href="#" aria-label="Instagram">IG</a>
    </div>
  </div>
</div>

<header class="sticky-header">
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

### CSS для "липкої" навігації

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
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Верхня інформаційна панель */
.pre-header {
  background-color: #f5f5f5;
  padding: 10px 0;
  font-size: 14px;
}

.contact-info a, .social-links a {
  text-decoration: none;
  color: #777;
  margin-right: 15px;
}

.contact-info a:hover, .social-links a:hover {
  color: #333;
}

/* Липка навігаційна панель */
.sticky-header {
  position: sticky;
  top: 0;
  background-color: #ffffff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  height: 70px;
  /* Для Safari */
  position: -webkit-sticky;
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

### JavaScript для покращення "липкої" навігації

```javascript
// Додавання класу при прокрутці для візуальних ефектів
window.addEventListener('scroll', () => {
  const stickyHeader = document.querySelector('.sticky-header');
  if (window.scrollY > 50) {
    stickyHeader.classList.add('scrolled');
  } else {
    stickyHeader.classList.remove('scrolled');
  }
});

// Мобільне меню
const mobileMenuToggle = document.querySelector('.mobile-menu-toggle');
const mainNav = document.querySelector('.main-nav');

mobileMenuToggle.addEventListener('click', () => {
  mainNav.classList.toggle('active');
});
```

### Додатковий CSS для анімації при прокрутці

```css
.sticky-header {
  transition: background-color 0.3s, box-shadow 0.3s, height 0.3s;
}

.sticky-header.scrolled {
  height: 60px;
  background-color: rgba(255, 255, 255, 0.95);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}
```

### Ключові аспекти позиціонування

1. **"Липке" позиціонування**:
   - `position: sticky` (з префіксом `-webkit-sticky` для Safari) дозволяє навігаційній панелі "прилипати" до верху екрану при прокрутці.
   - `top: 0` визначає точку, де панель починає "прилипати".

2. **Переваги над фіксованим позиціонуванням**:
   - Не потрібно додавати компенсуючий відступ для контенту, як у випадку з `position: fixed`.
   - Навігаційна панель займає своє нормальне місце в потоці документа, доки не "прилипне".
   - Більш природна поведінка для користувачів - панель видно тільки тоді, коли це дійсно потрібно.

3. **Динамічна зміна стилів**:
   - За допомогою JavaScript додаємо клас `scrolled` при прокрутці, що дозволяє змінювати стилі панелі (висоту, прозорість, тіні).
