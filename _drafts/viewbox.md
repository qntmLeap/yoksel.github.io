---
layout: default
title: SVG-viewbox
type: post
image:
desc:

---
Возможность гибко управлять размерами - одна из замечательных особенностей векторной графики. Помимо привычных ширины и высоты, в SVG есть ещё два параметра, задающие размеры отображаемого объекта. <!--more-->

Если вставить SVG на страницу без указания размеров, все браузеры отобразят его по-разному:

<p data-height="268" data-theme-id="4974" data-slug-hash="DIsLx" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/yoksel/pen/DIsLx/'>DIsLx</a> by yoksel (<a href='http://codepen.io/yoksel'>@yoksel</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Вы можете открыть a

в вебкитах SVG займет 100% ширины и высоты видимой области, в Firefox изображение получит размеры 300х200, в старой опере - 100% по ширине видимой области и 150px по высоте. ИЕ??? Вобщем, чтобы избежать сюрпризов в отображением, размеры нужно задавать явно.

SVG очень интересно работает с размерами. С помощью различных параметров можно управлять масштабированием как всего файла, так и отдельных его составляющих.
Тема сложная, но очень интересная.

<!--more-->
Спецификация <a href="http://www.w3.org/TR/SVG11/coords.html">w3.org/TR/SVG11/coords.html</a>

Если вставить на страницу SVG без указания размеров, все браузеры по своему зададут размеры картинки. В Firefox это прямоугольник 300х150, в старой опере - 100%х150px, в вебкитах SVG займет весь экран, причем каждая следующая картинка будет также иметь размеры 100%х100%.
Размеры нужно задавать явно, контент SVG не влияет на размер файла.

Viewport - видимая область просмотра, исходя из её размеров рассчитывается внутренняя система координат.


Если же нужно, чтобы SVG-картинка была определенного размера, можно задать ширину и высоту:

Если же задать не задавать ширину и высоту изображению, но задать их для контейнера - картинка будет ограничена размерами контейнера.

Если нужно чтобы картинка тянулась - viewbox
