---
layout: default
title: SVG-градиенты
type: post
image: https://img-fotki.yandex.ru/get/60436/5091629.a4/0_90849_6897689d_orig
desc: 'В SVG не работают привычные CSS-фоны, для заливок здесь есть свои конструкции. Для градиентов это элементы linearGradient и radialGradient — линейный и радиальный градиенты соответственно.'

tags: [svg, gradients]

post_nav:
- url: '#stops'
  name: 'Управление цветами'
- url: '#linear'
  name: 'Линейный градиент'
- url: '#radial'
  name: 'Радиальный градиент'
- url: '#gradientUnits'
  name: 'gradientUnits'
- url: '#gradientTransform'
  name: 'gradientTransform'
- url: '#spreadMethod'
  name: 'spreadMethod'
- url: '#xlink:href'
  name: 'xlink:href'
- url: '#pitfalls'
  name: 'Подводные камни'
- url: '#demos'
  name: 'Примеры использования'

---

В SVG не работают привычные CSS-фоны, для заливок здесь есть свои конструкции: для градиентов это элементы <code>linearGradient</code> и <code>radialGradient</code> — линейный и радиальный градиенты соответственно.<!--more-->

Спецификация: <a href="https://www.w3.org/TR/SVG/pservers.html#Gradients">w3.org/TR/SVG/pservers.html#Gradients</a>

CSS-градиенты объявляются прямо в CSS-коде, и код самого градиента потом нельзя переиспользовать. SVG-градиенты устроены иначе: перед использованием градиент должен быть описан с помощью соответствующего тега, и после этого его можно переиспользовать сколько угодно раз. И даже больше: градиенты могут наследовать свойства друг друга (об этом будет рассказано ниже).

Код самого простого градиента выглядит вот так:

<pre><code class="language-markup">&lt;linearGradient id="linear-gradient">
    &lt;stop offset="0%" stop-color="gold"/>
    &lt;stop offset="100%" stop-color="teal"/>
&lt;/linearGradient></code></pre>

Обязательный атрибут любого градиента — <code>id</code>.

Градиент не отображается на странице, пока не будет применён к элементу. Так же, как и обычная заливка или обводка, градиент задаётся с помощью <code>fill</code> или <code>stroke</code> — атрибутом элемента или через CSS.

Применим градиент к фигуре:

<pre><code class="language-markup">&lt;svg>
  &lt;!-- Градиент -->
  &lt;linearGradient id="linear-gradient">
    &lt;stop offset="0%" stop-color="gold"/>
    &lt;stop offset="100%" stop-color="teal"/>
  &lt;/linearGradient>

  &lt;!-- Фигура с градиентной заливкой -->
  &lt;rect fill="url(#linear-gradient)"
        width="100%" height="100%"/>
&lt;/svg></code></pre>

В действии:

<svg style="border: 1px solid #DDD">
  <linearGradient id="linear-gradient">
    <stop offset="0%" stop-color="gold"/>
    <stop offset="100%" stop-color="teal"/>
  </linearGradient>

  <rect fill="url(#linear-gradient)"
        width="100%" height="100%"/>
</svg>

Градиент можно использовать и как заливку и как обводку для фигур и для текста:

<p data-height="350" data-theme-id="4974" data-slug-hash="NAZgqo" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/NAZgqo/">NAZgqo</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<h3 id="stops">Управление цветами</h3>

Для управлениям цветами градиента служит элемент <code>stop</code>. Атрибуты:

<ul>
<li><code>offset</code> — положение цвета</li>
<li><code>stop-color</code> — цвет</li>
<li><code>stop-opacity</code> — прозрачность цвета</li>
</ul>

Пример кода:

<pre><code class="language-markup">&lt;stop offset=".25" stop-color="blue" stop-opacity=".5"/></code></pre>

Положение цвета задаётся в процентах или числом от 0 до 1 (50% и .5 будут работать одинаково).
Цвет и положение цвета указывать обязательно.

Интересно, что в отличие от CSS-градиентов, цвета SVG-градиентов можно анимировать (в данном случае, с помощью CSS):

<p data-height="300" data-theme-id="4974" data-slug-hash="bpXVpz" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/bpXVpz/">Animated SVG-gradient</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Линейный и радиальный градиенты имеют несколько общих свойств, но различаются способами, которыми задаются размер и направление градиента. Рассмотрим их поподробнее.

<h3 id="linear">Линейный градиент</h3>

Задаётся с помощью тэга <code>linearGradient</code>.

Вектор градиента задаётся с помощью атрибутов <code>x1</code>, <code>y1</code>, <code>x2</code> и <code>y2</code>.

<code>x1</code> и <code>y1</code> задают координаты начала вектора, <code>x2</code> и <code>y2</code> — координаты конца (похоже на рисование линии с помощью тега <code>line</code>).

<p data-height="500" data-theme-id="4974" data-slug-hash="NAamgv" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/NAamgv/">Gradient Coords: x2 & y2</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Если координаты не заданы, рисуется горизонтальный градиент слева направо.

Кнопки вверху демо переключают свойство <code>gradientUnits</code>, отвечающее за систему координат, подробнее о нём будет рассказано <a href="#gradientUnits">ниже</a>.

<h3 id="radial">Радиальный градиент</h3>

Задаётся с помощью тега <code>radialGradient</code>.

Параметры градиента задаются с помощью тех же атрибутов, что определяют свойства круга (элемента <code>circle</code>): центр фигуры задаётся атрибутами <code>cx</code> и <code>cy</code>, а радиус — атрибутом <code>r</code>:

<p data-height="470" data-theme-id="4974" data-slug-hash="KryqQz" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/KryqQz/">Gradient Coords: r</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Если какой-то из этих атрибутов не задан, ему присвоится значение по умолчанию, равное <code>50%</code>.

Помимо этого, у радиального градиента есть пара специфических свойств: <code>fx</code> и <code>fy</code>. Они позволяют сдвинуть только центр градиента, не затрагивая расположение конечных цветов:

<p data-height="470" data-theme-id="4974" data-slug-hash="kXxwqo" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/kXxwqo/">Gradient Coords: fx & fy</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Если эти атрибуты не заданы, их значения по умолчанию будут равны <code>cx</code> и <code>cy</code> соответственно.

<h3 id="common-props">Общие свойства градиентов</h3>

<h4 id="gradientUnits">gradientUnits</h4>

Это очень важное свойство, оно задаёт систему координат для атрибутов, отвечающих за направление и размеры градиента (<code>x1</code>, <code>y1</code>, <code>x2</code> и <code>y2</code> для линейных градиентов и <code>cx</code>, <code>cy</code>, <code>r</code>, <code>fx</code> и <code>fy</code> для радиальных).

Возможные значения:

<code>objectBoundingBox</code> — координаты рассчитываются относительно объекта, к которому применяется градиент. Значение по умолчанию.
<code>userSpaceOnUse</code> — координаты рассчитываются относительно системы координат всего SVG-элемента.

Помимо того, что при переключении <code>gradientUnits</code> градиент может менять своё положение из-за смены системы координат, это свойство также может существенно влиять на отрисовку градиента для фигур с разными шириной и высотой (например, вытянутый прямоугольник или эллипс).

При значении <code>userSpaceOnUse</code> цвета линейного градиента всегда будут перпендикулярны основному вектору, а радиальный градиент будет иметь форму круга. Но если градиент задан вытянутой фигуре, а значение <code>gradientUnits</code> равно <code>objectBoundingBox</code>, градиент пытается уместиться в фигуру целиком и подвергается искажениям. Особенно это заметно на радиальных градиентах:

<p data-height="470" data-theme-id="4974" data-slug-hash="WxaKdw" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/WxaKdw/">gradientUnits (radialGradient)</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

У линейных градиентов в этом случае меняется угол расположения цветов градиента относительно его вектора:

<p data-height="430" data-theme-id="4974" data-slug-hash="BzBzYG" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/BzBzYG/">gradientUnits</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Так что даже если системы координат фигуры и SVG-элемента совпадают, из-за разных значений <code>gradientUnits</code> градиент может выглядеть по-разному.


<h4 id="gradientTransform">gradientTransform</h4>

Атрибут позволяет задать трансформациии градиента:

<p data-height="470" data-theme-id="4974" data-slug-hash="bZAvxg" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/bZAvxg/">gradientTransform</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Трансформации <a href="/svg-shapes/">те же</a>, что и для обычных фигур, например, градиент можно повернуть или растянуть, но в трансформациях градиентов есть некоторые подводные камни.

Для градиентов, как и для всех прочих элементов, по умолчанию трансформации производятся относительно верхнего левого угла документа. Если требуется переопределить центр трансформации, нужно задать <code>transform-origin</code>. Явно в атрибуте его можно задать только для <code>rotate</code> (например, <code>rotate(180, 100, 100)</code>, два последних числа — это оно), для других трансформаций <code>transform-origin</code> будет работать только если он вместе с трансформацией задан в CSS. Но <code>gradientTransform</code> нельзя задать через CSS, следовательно <code>transform-origin</code> так тоже задать не получится. В этом случае можно использовать центрирование через <code>translate</code> (за подсказку спасибо <a href="https://twitter.com/AmeliasBrain/status/753284973210271744">@AmeliasBrain</a>):

<pre><code class="language-markup">translate(x,y) scale(s) translate(-x,-y).</code></pre>

В случае с радиальным градиентом вместо <code>scale</code> будет удобнее управлять радиусом градиента.

<h4 id="spreadMethod">spreadMethod</h4>

Этот атритбут управляет поведением градиента, если градиент меньше, чем область отрисовки.

Возможные значения:

<code>pad</code> — свободное пространство заполняется крайними цветами. Значение по умолчанию.
<code>reflect</code> — градиент отражается.
<code>repeat</code> — градиент повторяется.

<p data-height="570" data-theme-id="4974" data-slug-hash="YWANyJ" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/YWANyJ/">SpreadMethods for SVG Gradients</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<code>spreadMethod</code> не работает в Safari. Если надо чтобы везде работало, линейные повторяющиеся и отражённые градиенты можно имитировать с помощью паттернов, а повторение радиальных всё-таки придётся прописывать руками.

<h4 id="xlink-href">xlink:href</h4>

Этот атрибут позволяет градиентам заимствовать друг у друга цвета и свойства. Если в градиенте, содержащем атрибут <code>xlink:href</code>, не заданы цвета, они унаследуются из градиента по ссылке. Также из заданного градиента унаследуются все свойства, которые не переопределены в текущем градиенте. При этом радиальные градиенты могут наследовать цвета и свойства линейного, и наоборот.

Вот пример использования:

<pre><code class="language-markup">&lt;!-- Исходный линейный градиент -->
&lt;linearGradient id="linear-gradient">
    &lt;stop offset="0%" stop-color="crimson"
          class="stop-1"/>
    &lt;stop offset="49%" stop-color="gold"
          class="stop-2"/>
    &lt;stop offset="50%" stop-color="lemonchiffon"
          class="stop-2"/>
    &lt;stop offset="51%" stop-color="gold"
          class="stop-2"/>
    &lt;stop offset="100%" stop-color="teal"
          class="stop-3"/>
&lt;/linearGradient>

&lt;!-- Радиальный градиент, наследующий цвета и свойства линейного -->
&lt;radialGradient id="radial-gradient"
    xlink:href="#linear-gradient">
&lt;/radialGradient></code></pre>

Код в действии, радиальный градиент справа унаследовал цвета линейного градиента слева:

<p data-height="470" data-theme-id="4974" data-slug-hash="jAaazW" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/jAaazW/">Gradient properties inheritance</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

В этом демо к градиенту слева применяется трансформация, и она также наследуется градиентом справа.

<h3 id="pitfalls">Подводные камни</h3>

Градиент можно использовать в качестве заливки и обводки, и задавать его можно как атрибутами <code>fill</code> и <code>stroke</code>, так и в CSS. При этом можно сложить градиенты в отдельный файл, и подключать их оттуда, это избавит от необходимости вставлять градиенты в тело документа.

К сожалению, все самые удобные и интересные способы не очень хорошо поддерживаются браузерами. Так, в CSS запись вида <code>fill: url(#grad);</code> подразумевает, что градиент с таким ID нужно искать в текущем документе. В Хроме, Опере и Сафари всё так и происходит, однако Firefox начинает искать градиент относительно расположения файла со стилями, и ожидаемо ничего не находит. Можно привести ссылку в CSS в соответствие с адресом страницы, но это не поможет, если страниц больше одной.

Запись вроде <code>fill: url(svg-with-gradients.svg#gradient);</code> указывает, что градиент нужно брать из внешнего файла, и это было бы суперудобно, но, к сожалению, работает только в Firefox.

Таким образом, самый надёжный способ — это задавать градиент используя атрибуты элемента.

<h3 id="demos">Примеры использования</h3>

SVG-градиенты сами по себе дают интересные возможности оформления, но ещё интереснее то, как они работают в сочетании с масками. Например, используя маски и градиенты можно сделать вот такие мыльные пузыри:

<p data-height="500" data-theme-id="4974" data-slug-hash="EyZgLo" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/EyZgLo/">SVG Bubbles</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<a href="http://codepen.io/yoksel/full/BzkyBJ">Тут есть подробная схема отдельного пузыря.</a>

Также анимируя градиенты можно делать разные интересные штуки. Например, вот такой паттерн (цвета анимируются с помощью CSS):

<p data-height="400" data-theme-id="4974" data-slug-hash="VjZGGg" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/VjZGGg/">Animated pattern with SVG gradient</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Или переливающийся текст:

<p data-height="300" data-theme-id="4974" data-slug-hash="RRLXKP" data-default-tab="result" data-user="yoksel" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/yoksel/pen/RRLXKP/">Text with gradientTransform</a> by yoksel (<a href="http://codepen.io/yoksel">@yoksel</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Анимацию цветов можно сделать с помощью CSS, трансформации можно добавить только с помощью JavaScript (я это делаю с помощью библиотеки <a href="https://greensock.com/get-started-js">GSAP</a>).

