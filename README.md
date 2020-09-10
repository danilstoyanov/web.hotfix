# ❗ Информация для проверяющих специалистов 
В задании исправлены все 5 багов. Для удобства проверки, ниже я расписал в чем заключался баг и какие меры были приняты чтобы пофиксить его<br />

## Тестовый стенд
[http://mega-web-hotfix.surge.sh/](http://mega-web-hotfix.surge.sh/)<br />

## Баг #1
**Описание бага:** пользователь может создать пустой заказа <br />
**Ссылка на коммит:** [e10fd0e22a0f2f8e710d44aaa9cc54e4679375b1](e10fd0e22a0f2f8e710d44aaa9cc54e4679375b1) <br />
**Решение:** добавлена дополнительная проверка на наличие товаров из выбранного магазина в объекте ```order```. По результатам проверки рендерится либо обычный ```<a>``` (при клике на которую переход не случается) либо ```<Link>```.<br /> **Также при попытке перейти в корзину с пустым заказом будет РЕДИРЕКТ на главную страницу!**

## Баг #2
**Описание бага:** при указании времени доставки можно ввести всё что угодно<br />
**Ссылка на коммит:** [2d26304f0dcb22b13f38afc65076a96506f790c3](2d26304f0dcb22b13f38afc65076a96506f790c3) <br />
**Решение:** самое простое решение использовать ```input``` с аттрибутом ```type="time"```. Хотя такое решение и не будет работать в ```Safari```, но организаторы в орг чате сказали что проверка задания будет только в ```Google Chrome```. Поэтому я решил использовать это минимальное решение

## Баг #3
**Описание бага:** цена картофеля фри отличается в меню и при оформлении заказа<br />
**Ссылка на коммит:** [810b357255dd625210b952f70ef94a10a43c0824](810b357255dd625210b952f70ef94a10a43c0824) <br />
**Решение:** нужно было обратить внимание на ключ в объекте товаров, картошка имела ключ ```bigmac```, из-за этого ей выставлялась цена бигмака. Пофиксил заменой ключа с ```bigmac``` на ```fried```

## Баг #4
**Описание бага:** после отмены заказа в консоли приходит статус DONE вместо CANCELED<br />
**Ссылка на коммит:** [bb79e5672693f44cef6737c635e1eb021e441454](bb79e5672693f44cef6737c635e1eb021e441454) <br />
**Решение:** я добавил новый метод ```setCanceledOrder```, который срабатывает при клике на кнопку ```Отм.``` и присваивает текущей позиции статус ```CANCELED```

## Баг #5
**Описание бага:** сброс параметров заказа при редактировании<br />
**Ссылка на коммит:** [64712fdb15e765f75b7289563f8bb0edefc5333c](64712fdb15e765f75b7289563f8bb0edefc5333c) <br />
**Решение:** по аналогии с логикой приложения, я добавил хранение промежуточное состояния формы в ```localStorage```. Это обеспечивает синхронизацию настроек заказа при переходу к редактированию и обратно, а также при перезагрузке страницы
