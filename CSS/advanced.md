10 верных ответов из 15 (тест пройден, 09.2025)
Вот список всех 15 вопросов с вариантами ответов и правильными ответами:

## 1. Как выбрать только те элементы `<p>`, которые находятся непосредственно внутри `<div class="d">`?

<div class="a">
  <div class="b">
    <p class="c">text</p>
  </div>
  <div class="d">
    <p class="e">text</p>
  </div>
  <div class="f">
    <span class="g">Text</span>
  </div>
</div>

Варианты ответов:

1. `.d > p`
2. `div.d .e`
3. `div.d > e.p`
4. `div > .e`
5. `.d p`

**Правильный ответ:** `.d > p`

## 2. Как корректно сделать все текстовые элементы в `<main>` унаследованными от `font-family`, заданного на `<body>`?

Варианты ответов:

1. `body > main { font-family: initial !important; }`
2. `main { font-family: none; }`
3. `main * { all: inherit; }`
4. `main * { font-family: unset !important; }`
5. `main { all: unset; font-family: inherit; }`

**Правильный ответ:** `main * { font-family: unset !important; }`

## 3. Как добавить логотип (размеры исходного изображения 40 x 40 пикселей) на страницу через тег `img` для адаптивной верстки?

Варианты ответов:

1. Задать `flex-basis`
2. Дополнительных действий совершать не нужно
3. Сделать `img` блочным тегом
4. Сделать `img` строчным тегом
5. Ограничить ширину и высоту

**Правильный ответ:** Задать `flex-basis`

## 4. Когда может быть оправдано динамическое добавление CSS через JavaScript?

Варианты ответов:

1. Когда нужно изменять стили в зависимости от событий
2. Когда проект требует строгого разделения логики и представления
3. Когда проект не использует JavaScript вовсе
4. Когда необходимо обеспечить поддержку всех старых браузеров
5. Когда нужно сократить размер финального HTML-файла

**Правильный ответ:** Когда нужно изменять стили в зависимости от событий

## 5. Как задать фиксированную ширину поля ввода для ввода ровно 30 символов среднего размера?

Варианты ответов:

1. Использовать `min-width: 30vw`
2. Использовать `width: 30ex`
3. Использовать `width: 30ch`
4. Использовать `max-width: 30rem`
5. Использовать `width: 30em`

**Правильный ответ:** Использовать `width: 30ch`

## 6. Как выровнять элементы по центру горизонтально и задать равные промежутки между ними при помощи Flexbox?

Варианты ответов:

1. Использовать `display: flex; justify-content: flex-start; margin-right: auto`
2. Использовать `text-align: center` на контейнер и `padding` на элементы
3. Применить `display: flex; justify-content: space-between; margin: 16px`
4. Применить `display: flex; align-items: center; padding: 16px`
5. Использовать `display: flex; justify-content: center; gap: 16px`

**Правильный ответ:** Использовать `display: flex; justify-content: center; gap: 16px`

## 7. Что определяет свойство `flex-shrink` в контексте Flexbox?

Варианты ответов:

1. Отступы между элементами внутри контейнера
2. Максимальное количество строк, которые может занять элемент
3. Приоритет элемента при уменьшении доступного пространства
4. Скорость анимации сжатия элемента
5. Уровень прозрачности при изменении размера

**Правильный ответ:** Приоритет элемента при уменьшении доступного пространства

## 8. Как добавить иконку после текста кнопки без изменения HTML-разметки?

Варианты ответов:

1. Добавить `::after + content`
2. Задать `::marker` содержимое
3. Применить `:has()` к кнопке
4. Применить `:focus-visible`
5. Использовать `::before` без `content`

**Правильный ответ:** Добавить `::after + content`

## 9. Какой из следующих CSS-селекторов выберет каждый чётный элемент списка `<li>`, при этом начиная с нуля?

Варианты ответов:

1. `li:nth-of-type(odd)`
2. `li:nth-child(even)`
3. `li:nth-last-child(2n)`
4. `li:nth-child(2n+1)`
5. `li:nth-child(odd)`

**Правильный ответ:** `li:nth-child(2n+1)`

## 10. Как реализовать функцию reduce motion для выключения всех анимаций и переходов на странице, используя `@keyframes` и CSS?

Варианты ответов:

1. `{ transition-duration: 0; animation: none; }`
2. `{ transition-delay: 0 !important; animation: none; }`
3. `{ transition-property: none; animation: none !important; }`
4. `{ transition-timing-function: ease; animation: none; }`
5. `{ transition-duration: 0 !important; animation: none !important; }`

**Правильный ответ:** `{ transition-duration: 0 !important; animation: none !important; }`

## 11. Как добиться эффекта увеличения элемента вперёд из плоскости экрана с помощью CSS 3D трансформаций?

Варианты ответов:

1. `transform: translate(100px)`
2. `transform: skewZ(100deg)`
3. `transform: rotate3d(0, 0, 1, 90deg)`
4. `transform: matrix(1, 0, 0, 1, 0, 0)`
5. `transform: scale(2)`

**Правильный ответ:** `transform: translateZ(100px)`

## 12. В каком случае элемент при позиционировании НЕ вызовет пересчёт родительского layout при смещении?

Варианты ответов:

1. `position: relative; top: 10px`
2. `padding-top: 10px`
3. `transform: translateY(10px)`
4. `margin-top: 10px`
5. `top: 10px`

**Правильный ответ:** `transform: translateY(10px)`

## 13. Выберите вариант с наименьшим весом селекторов (приоритетом).

Элемент: `<p class="text sample test" id="test"></p>`

Варианты ответов:

1. `p.sample#test`
2. `p.test#test`
3. `p#test.sample`
4. `p.text.sample`
5. `.text.sample.test`

**Правильный ответ:** `p#test.sample`

## 14. Как правильно сделать так, чтобы содержимое блока не выходило за границы экрана и появлялся скролл только по горизонтали?
.wrapper {
    ???;
}

Варианты ответов:

1. `overflow: auto; width: 100vw;`
2. `text-overflow: ellipsis; overflow: auto;`
3. `scroll-behavior: smooth; overflow: visible;`
4. `overflow-x: scroll; white-space: nowrap;`
5. `overflow: hidden`

**Правильный ответ:** `overflow-x: scroll; white-space: nowrap;`

## 15. Что произойдёт с изображением, если экран будет меньше 768px?

```css
img {
  width: 100%;
  height: auto;
}
@media (max-width: 768px) {
  img {
    object-fit: cover;
    height: 300px;
  }
}
```

Варианты ответов:

1. Изображение сохранит пропорции
2. Изображение растянется на весь экран
3. Изображение будет сжато по высоте
4. Изображение будет обрезано по высоте
5. Изображение исчезнет

**Правильный ответ:** Изображение будет сжато по высоте

/////////////////////////////////////////////////////////////////////
УСТАРЕВШИЕ ВОПРОСЫ (05.2025)

13 верных ответов из 15 (тест пройден).

Вопрос 1.
Вы работаете над карточкой товара для интернет-магазина. Вам нужно добавить рамку толщиной 2px, отступ внутри элемента в 10px и внешний отступ в 15px. Какой будет итоговая ширина карточки, если исходная ширина блока равна 200px и используется значение по умолчанию для box-sizing?

Ответы:

1. 228px
2. 234р
3. 248px
4. 224px
5. 214px

Ответ 4
//этот ответ точно правильный

Вопрос 2.
Вы разрабатываете блок с карточками для сайта. Все карточки размещены внутри многострочного флекс- контейнера с фиксированной высотой 500px. Вам нужно выровнять строки карточек по центру поперечной оси контейнера, чтобы они были расположены равномерно посередине. Какое СЅЅ-свойство вы примените для достижения такого выравнивания?

Ответы:

1. align-self: center
2. align-items: center
3. flex-wrap: center
4. justify-content: center
5. align-content: center

Ответ 5.

Вопрос 3.
Вы создаете таблицу с данными. Вам нужно выделить все ячейки второго столбца, которые находятся в четных строках, а также закрасить последнюю строку таблицы независимо от числа ее ячеек. Какой СЅЅ-код вы примените, чтобы решить поставленную задачу?

<table>
<tr>
    <td>Строка 1, Ячейка 1</td>
    <td>Строка 1, Ячейка 2</td>
</tr>
<tr>
    <td>Строка 2, Ячейка 1</td>
    <td>Строка 2, Ячейка 2</td>
</tr>
<!-- Больше строк ->
</table>

Ответы:

1. tr:nth-child(even) td:last-child { background-color: #ddd;}
2. tr:nth-of-type(even) td:nth-child(2) { background-color: #ddd;}
3. tr:last-of-type td{ background-color: #ddd;}
4. tr:nth-child(odd):last-child td { background-color: #ddd; }
5. tr:nth-of-type(even) td:nth-of-type(2), tr:last-child td { background-color: #ddd;}

Ответ 5.

Вопрос 4.
Проанализируйте код ниже и определите, какие стили будут применяться к элементу с классом. highlight, если
он следует за элементом с классом .item, находящимся в контейнере .container?

.container .item + .highlight {
background-color: yellow;
}
.container > .item + .highlight {
color: red;
}
.container .item ~ .highlight {
font-weight: bold;
}

.container > .item ~ .highlight {
text-decoration: underline;
}
.container > .item + .highlight {
font-style: italic;
}

Ответы:

1. Все стили из кода применятся к элементу
2. font-weight: bold и color: red:
3. font-style: italic и color: red:
4. color: red и background-color: yellow
5. background-color: yellow, font-style: italic; и color: red;

Ответ 1.
//этот ответ точно правильный

Вопрос 5.
Вы нужно сделать так, чтобы последний элемент в контейнере с display: flex занимал всю оставшуюся ширину. но не менее 200px, в то время как остальные элементы были фиксированной ширины. Какой стиль необходимо добавить к последнему элементу для достижения этого результата?
container {
display: flex;
}
.item {
width: 150px;
}
.last-item {
width: 200px;
/_ Какие стили добавить? _/
}

Ответы:

1. flex-grow: 2; width: auto;
2. flex-grow: 1; flex-shrink: 0:
3. align-self: stretch: flex-grow: 1;
4. flex-basis: 100%; flex-grow: 0;
5. width: auto; flex-shrink: 0;

Ответ 2.

Вопрос 6.
Вам нужно создать анимацию, в которой текст на экране сначала плавно перемещается справа налево и увеличивается, после этого исчезает. Однако при тестировании вы замечаете, что текст перемещается и исчезает сразу, без ожидаемого завершения эффекта движения. Что нужно сделать, чтобы исправить данную анимацию?

.text{
animation: text-move 4s ease-in-out forwards;
}
@keyframes text-move {
0% {
transform: translateX(100px) scale(1);
opacity: 1;
}
50% {
transform: translateX(0) scale(1.5);
}
100% {
opacity:0;
}
}

Ответы:

1. Добавить animation-delay: 2s; к анимации, чтобы масштабирование и исчезновение начались позже
2. Указать transform: translateX(0) scale(1.5); в 100% кадре, чтобы сохранить увеличенный размер
3. Добавить transform: scale(1); в 100% кадр, чтобы движение и исчезновение завершались одновременно
4. Добавить в 50% кадр opacity: 1;, чтобы исчезновение началось только в конце анимации
5. Переместить оpacity: 0; в 50% кадр, чтобы элемент начал исчезать

Ответ 2.

Вопрос 7.
Вам нужно подключить дополнительное фоновое изображение для дисплеев на сайте. Плотность пикселей дисплеев составляет 2х. Какое медиавыражение необходимо использовать для подключения такого
изображения?

Ответы:

1. @media (max-resolution: 180dpi) { background-image: url('image@2x.png'); }
2. @media (min-device-pixel-ratio: 3) { background-image: url('image@2x.png'); }
3. @media (min-resolution: 2dppx) { background-image: url('image@2x.png'); }
4. @media (max-device-pixel-ratio: 2) { background-image: url('image@2x.png"); }
5. @media (min-resolution: 112dpi) { background-image: url('image@2x.png' ); }

Ответ 3.

Вопрос 8.
В чем отличие директивы @mixin от директивы @include в ЅСЅЅ?

Ответы:

1. @mixin используется для медиазапросов, а include для обычных CSS правил
2. @mixin создаёт общие стили, а @include добавляет эти стили к выбранным элементам
3. @include поддерживает вложенные селекторы, а @mixin - нет
4. @include позволяет определять стили, а @mixin — вставляет их в код
5. B @mixin можно использовать параметры, а @include - это CSS правило без параметров

Ответ 2.

Вопрос 9.
Какой из вариантов кода корректно подключает миксин center с передачей значений для элемента в ЅСЅЅ- коде?
@mixin center($width, $height){
width: $width;
height: $height;
display: flex;
justify-content: center;
align-items: center;
}

Ответы:

1. @mixin center(Swidth: 100%, Sheight: 100%);
2. @include center(100, 100);
3. @include center(Swidth-100px, Sheight-100px):
4. @mixin center(100px', '100px");
5. @include center(100%, 100%);

Ответ 5.

Вопрос 10.
Вам нужно создать сетку из карточек, как показано на изображении ниже. Макет состоит из нескольких колонок и разной ширины карточек. Что нужно сделать, чтобы правильно реализовать данную сетку?

Ответы:

1. Родительскому блоку задать display: grid; grid-template-columns: repeat(3, 1fr);, а широким широким карточкам задать модификатор и добавить свойство grid-column: span 2;
2. Родительскому блоку задать display: grid; grid-template-columns: repeat(4, 1fr); а широким карточкам задать модификатор и добавить свойство grid-column: span 2;
3. Родительскому блоку задать display: grid; grid-template-columns: auto;, а всем карточкам назначить фиксированную ширину
4. Родительскому блоку задать display: grid; grid-template-columns: переat(3, 2fr); а всем карточкам сделать автоматически распределяться по сетке
5. Родительскому блоку задать display: flex; flex-wrap: wrap; а широким карточкам увеличить ширину в два раза с помощью модификатора

Ответ 1.

Вопрос 11.
Вы создаете адаптивную сетку карточек для интернет-магазина. Задача состоит в следующем: на больших экранах карточки размещаются по три в строке, а при уменьшении ширины экрана карточки должны автоматически переноситься на следующую строку, если их ширина становится меньше 200px. При этом карточки в строке должны равномерно распределять оставшееся пространство.
Какой из следующих вариантов CSS-кода решает данную задачу?

Ответы:

1. grid-template-columns: minmax(200px, 1fr)
2. grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
3. grid-template-columns: 1fr 1fr 1fr;
4. grid-template-columns: repeat(3, 1fr);
5. grid-template-columns: repeat(auto-fill, 200px);

Ответ 2.

Вопрос 12.
Какое из предложенных действий наиболее эффективно ускоряет загрузку веб-шрифтов?

Ответы:

1. Загрузка шрифтов после завершения рендеринга страницы
2. Использование системных шрифтов вместо веб-шрифтов
3. Использование свойства display: swap в CSS для шрифтов
4. Подключение веб-шрифтов с использованием @import внутри СЅЅ
5. Подключение всех возможных начертаний шрифтов в проекте

Ответ 3.

Вопрос 13.
При разработке блока на сайте вы столкнулись с задачей, где вам необходимо увеличить элемент на 20% и сдвинуть его вверх на 30px. Выберите СЅЅ-код, который поможет решить данную задачу.

Ответы:

1. transform: scale(20%) translate(30px, 0);
2. transform: translate(0,-30px) scale(1.2);
3. transform: translate(30px) scale(1.2);
4. transform: translate(0, 30px) scale(20%);
5. transform: scale(1.2) translate(30px, 0);

Ответ 2.

Вопрос 14.
Проанализируйте код и определите, какой цвет применился к элементу <p>.

//HTML

<div class="container" id="main">
    <div class="box" id="primary">
        <p class="text special">Какой будет цвет у данного текста?</p>
    </div>
</div>
/CSS
.container .box {color: red;}
#main #primary .special {color: blue;}
.text.special {color: green;}
div#main .box .text {color: orange;}
.container #primary .text {color:purple;}

Ответы:

1. color: blue;
2. color: purple;
3. color: orange;
4. color: green;
5. color: red;

Ответ 1.

Вопрос 15.
Какой из следующих факторов НЕ создает новый контекст наложения (stacking context) в CSS?

Ответы:

1. Элемент с оpacity менее 1
2. Элемент c transform отличным от попе
3. Элемент с position: absolute и z-index отличным от auto
4. Элемент с рosition: relative и z-index отличным от auto
5. Элемент с роsition: static и z-index отличным от auto

Ответ 5.
