# CSS Анімації

## 1. Ключові кадри (@keyframes)

### 1.1. Синтаксис @keyframes
```css
@keyframes назва-анімації {
    from {
        /* початковий стан */
    }
    to {
        /* кінцевий стан */
    }
}

/* або з використанням відсотків */
@keyframes назва-анімації {
    0% {
        /* початковий стан */
    }
    50% {
        /* проміжний стан */
    }
    100% {
        /* кінцевий стан */
    }
}
```

### 1.2. Приклад простої анімації
```css
@keyframes rotate {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}
```

## 2. Властивості анімації

### 2.1. Основні властивості
```css
.element {
    /* Базовий синтаксис */
    animation: назва-анімації 1s ease infinite;

    /* Розширений запис */
    animation-name: назва-анімації;         /* назва анімації */
    animation-duration: 1s;                  /* тривалість */
    animation-timing-function: ease;         /* функція часу */
    animation-delay: 0s;                    /* затримка */
    animation-iteration-count: infinite;     /* кількість повторень */
    animation-direction: normal;            /* напрямок */
    animation-fill-mode: forwards;          /* режим заповнення */
    animation-play-state: running;          /* стан відтворення */
}
```

### 2.2. Значення властивостей

#### animation-timing-function
```css
.element {
    animation-timing-function: linear;      /* рівномірна швидкість */
    animation-timing-function: ease;        /* плавний початок і кінець */
    animation-timing-function: ease-in;     /* плавний початок */
    animation-timing-function: ease-out;    /* плавний кінець */
    animation-timing-function: ease-in-out; /* плавний початок і кінець */
}
```

#### animation-direction
```css
.element {
    animation-direction: normal;          /* звичайний напрямок */
    animation-direction: reverse;         /* зворотний напрямок */
    animation-direction: alternate;       /* чергування напрямків */
    animation-direction: alternate-reverse; /* чергування зі зворотного */
}
```

#### animation-fill-mode
```css
.element {
    animation-fill-mode: none;      /* за замовчуванням */
    animation-fill-mode: forwards;  /* зберігає кінцевий стан */
    animation-fill-mode: backwards; /* застосовує початковий стан */
    animation-fill-mode: both;      /* обидва ефекти */
}
```

## 3. Практичні приклади

### 3.1. Пульсуюча кнопка
```css
@keyframes pulse {
    0% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.1);
    }
    100% {
        transform: scale(1);
    }
}

.pulse-button {
    padding: 10px 20px;
    background: #007bff;
    border: none;
    border-radius: 4px;
    color: white;
    animation: pulse 2s ease infinite;
}
```

### 3.2. Завантажувач (loader)
```css
@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

.loader {
    width: 40px;
    height: 40px;
    border: 4px solid #f3f3f3;
    border-top: 4px solid #3498db;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}
```

### 3.3. Анімація появи елемента
```css
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.fade-in {
    animation: fadeIn 0.5s ease-out forwards;
}
```

## 4. Складні анімації

### 4.1. Комбінування декількох анімацій
```css
.element {
    animation: 
        slideIn 0.5s ease-out,
        fadeIn 0.5s ease-out,
        pulse 2s ease infinite;
}
```

### 4.2. Анімація з паузою при наведенні
```css
.animated-element {
    animation: bounce 1s infinite;
}

.animated-element:hover {
    animation-play-state: paused;
}
```

## 5. Поради та найкращі практики

1. **Продуктивність:**
   - Анімуйте тільки властивості `transform` та `opacity`
   - Використовуйте `will-change` для оптимізації
   
2. **Доступність:**
   - Враховуйте налаштування користувача `prefers-reduced-motion`
   ```css
   @media (prefers-reduced-motion: reduce) {
       .animated {
           animation: none;
       }
   }
   ```

3. **Оптимізація:**
   - Не анімуйте більше 3-4 властивостей одночасно
   - Уникайте анімацій, які можуть викликати перевантаження браузера

4. **Відлагодження:**
   - Використовуйте DevTools для налагодження анімацій
   - Перевіряйте продуктивність за допомогою Performance панелі
