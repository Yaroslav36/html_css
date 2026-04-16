# Навігаційні меню з використанням CSS позиціонування (Частина 3)

## 3. Випадаючі (dropdown) меню

Випадаючі меню - ідеальний приклад поєднання відносного та абсолютного позиціонування. Вони дозволяють економити простір на сторінці, ховаючи додаткові пункти меню, які відображаються при наведенні або кліку.

### HTML структура

```html
<header class="site-header">
  <div class="container">
    <a href="#" class="logo">Лого сайту</a>
    <nav class="main-nav">
      <ul class="menu">
        <li><a href="#home">Головна</a></li>
        
        <li class="dropdown">
          <a href="#products" class="dropdown-toggle">Продукти <span class="arrow">▼</span></a>
          <ul class="dropdown-menu">
            <li><a href="#category1">Категорія 1</a></li>
            <li><a href="#category2">Категорія 2</a></li>
            <li><a href="#category3">Категорія 3</a></li>
            <li><a href="#all-products">Всі продукти</a></li>
          </ul>
        </li>
        
        <li class="dropdown">
          <a href="#services" class="dropdown-toggle">Послуги <span class="arrow">▼</span></a>
          <ul class="dropdown-menu">
            <li><a href="#service1">Послуга 1</a></li>
            <li><a href="#service2">Послуга 2</a></li>
            <li><a href="#service3">Послуга 3</a></li>
          </ul>
        </li>
        
        <li><a href="#about">Про нас</a></li>
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

### CSS для випадаючих меню

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

/* Шапка сайту */
.site-header {
  background-color: #ffffff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  height: 70px;
  position: relative;
  z-index: 100;
}

/* Логотип */
.logo {
  font-size: 24px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}

/* Головне меню */
.menu {
  display: flex;
  list-style: none;
}

.menu > li {
  position: relative;
  margin-left: 20px;
}

.menu a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  padding: 10px 0;
  display: block;
  transition: color 0.3s;
}

.menu a:hover {
  color: #3498db;
}

/* Стрілка для випадаючих меню */
.arrow {
  font-size: 10px;
  margin-left: 5px;
  transition: transform 0.3s;
}

/* Випадаюче меню */
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background-color: #ffffff;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  min-width: 200px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(10px);
  transition: opacity 0.3s, visibility 0.3s, transform 0.3s;
  z-index: 101;
  border-radius: 4px;
  overflow: hidden;
}

.dropdown-menu li {
  list-style: none;
}

.dropdown-menu a {
  padding: 12px 15px;
  display: block;
  border-bottom: 1px solid #f1f1f1;
}

.dropdown-menu a:hover {
  background-color: #f9f9f9;
}

/* Активація випадаючих меню при наведенні */
.dropdown:hover .dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.dropdown:hover .arrow {
  transform: rotate(180deg);
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
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  }
  
  .main-nav.active {
    display: block;
  }
  
  .menu {
    flex-direction: column;
    padding: 20px;
  }
  
  .menu > li {
    margin: 0;
    margin-bottom: 15px;
  }
  
  .dropdown-menu {
    position: static;
    opacity: 1;
    visibility: visible;
    transform: none;
    box-shadow: none;
    min-width: auto;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s;
  }
  
  .dropdown.active .dropdown-menu {
    max-height: 1000px;
  }
  
  .mobile-menu-toggle {
    display: block;
  }
}
```

### JavaScript для мобільної версії

```javascript
// Мобільне меню
const mobileMenuToggle = document.querySelector('.mobile-menu-toggle');
const mainNav = document.querySelector('.main-nav');
const dropdowns = document.querySelectorAll('.dropdown');

mobileMenuToggle.addEventListener('click', () => {
  mainNav.classList.toggle('active');
});

// На мобільних: розкриття випадаючих меню по кліку
if (window.innerWidth <= 768) {
  dropdowns.forEach(dropdown => {
    const dropdownToggle = dropdown.querySelector('.dropdown-toggle');
    
    dropdownToggle.addEventListener('click', (e) => {
      // Запобігаємо переходу по посиланню при кліку на мобільному
      e.preventDefault();
      dropdown.classList.toggle('active');
    });
  });
}
```

### Ключові аспекти позиціонування

1. **Позиціонування батьківського елемента**:
   - `.menu > li { position: relative; }` створює контекст позиціонування для випадаючого меню.

2. **Абсолютне позиціонування випадаючого меню**:
   - `.dropdown-menu { position: absolute; top: 100%; left: 0; }` розміщує випадаюче меню безпосередньо під батьківським пунктом.
   - `z-index: 101` забезпечує відображення випадаючого меню над іншими елементами.

3. **Анімація появи**:
   - Комбінація `opacity`, `visibility` та `transform` створює плавну анімацію появи.
   - `.dropdown:hover .dropdown-menu { ... }` активує меню при наведенні.

4. **Адаптивність для мобільних пристроїв**:
   - На мобільних пристроях `.dropdown-menu { position: static; }` змінює абсолютне позиціонування на статичне, що розміщує випадаюче меню в потоці документа.
   - Використовується інший механізм розкриття через `max-height` замість `visibility` та `opacity`.

## 4. Рівні вкладеності у випадаючих меню

Для більш складних меню з декількома рівнями вкладеності використовується подібний підхід, але з кількома рівнями абсолютного позиціонування.

### HTML для багаторівневого меню

```html
<li class="dropdown">
  <a href="#products" class="dropdown-toggle">Продукти <span class="arrow">▼</span></a>
  <ul class="dropdown-menu">
    <li><a href="#category1">Категорія 1</a></li>
    <li class="dropdown-submenu">
      <a href="#category2" class="dropdown-toggle">Категорія 2 <span class="arrow-right">▶</span></a>
      <ul class="submenu">
        <li><a href="#subcategory1">Підкатегорія 1</a></li>
        <li><a href="#subcategory2">Підкатегорія 2</a></li>
        <li><a href="#subcategory3">Підкатегорія 3</a></li>
      </ul>
    </li>
    <li><a href="#category3">Категорія 3</a></li>
  </ul>
</li>
```

### Додатковий CSS для багаторівневих меню

```css
/* Стрілка для підменю */
.arrow-right {
  font-size: 10px;
  margin-left: 5px;
}

/* Підменю */
.dropdown-submenu {
  position: relative;
}

.submenu {
  position: absolute;
  top: 0;
  left: 100%;
  background-color: #ffffff;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  min-width: 200px;
  opacity: 0;
  visibility: hidden;
  transform: translateX(10px);
  transition: opacity 0.3s, visibility 0.3s, transform 0.3s;
  z-index: 102;
  border-radius: 4px;
  overflow: hidden;
}

.dropdown-submenu:hover .submenu {
  opacity: 1;
  visibility: visible;
  transform: translateX(0);
}

/* Медіа-запити для адаптивності */
@media (max-width: 768px) {
  .submenu {
    position: static;
    opacity: 1;
    visibility: visible;
    transform: none;
    box-shadow: none;
    padding-left: 20px;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s;
  }
  
  .dropdown-submenu.active .submenu {
    max-height: 1000px;
  }
}
```

### Ключові моменти багаторівневого меню

1. **Позиціонування підменю**:
   - Використовується `position: absolute; top: 0; left: 100%;` для розміщення підменю праворуч від батьківського пункту.
   - Збільшення значення z-index з кожним рівнем вкладеності забезпечує правильне накладання елементів.

2. **Мобільний режим**:
   - На мобільних пристроях меню перетворюється на звичайний список з відступами (`padding-left: 20px`) для відображення ієрархії.

## Висновок

Навігаційні меню демонструють, як різні типи позиціонування працюють разом для створення інтуїтивних інтерфейсів:

- `position: relative` створює контекст позиціонування для дочірніх елементів.
- `position: absolute` дозволяє точно розміщувати випадаючі меню відносно батьківських пунктів.
- `position: fixed` або `position: sticky` забезпечують постійний доступ до навігації при прокрутці.

Адаптивний дизайн вимагає різних підходів до позиціонування на різних пристроях, що яскраво демонструється зміною від абсолютного до статичного позиціонування на мобільних пристроях.
