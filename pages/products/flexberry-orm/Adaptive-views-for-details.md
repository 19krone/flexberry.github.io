---
title: Адаптивные представления для детейлов
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, View (представление)
toc: true
permalink: ru/fo_adaptive-views-for-details.html
folder: products/flexberry-orm/
lang: ru
---

<div style="margin:5px; padding-left:28px; float:right; width:40%; outline:1px solid white;">
<br>
<table border="0" width="100%" bgcolor="#6495ED">
<tbody><tr><td bgcolor="#FFFFFF">
* '''Продукт''': [Flexberry ORM](flexberry-o-r-m.html)
* '''Компонент''': [Представления (View)](view-definition.html)
* '''Программная библиотека''': ICSSoft.STORMNET.Business.dll
* '''Предназначение''': Для вычитки [объектов-наследников](inheritance.html) по более широкому набору свойств, нежели у [предков](inheritance.html), могут использоваться адаптивные представления.
</td>
</tr></tbody></table></a>
</div>
# Адаптивные представления
Допустим, что имеется следующая ситуация:
![](/images/pages/img/Учебник программиста Casseberry/primer5.jpg)
Класс A имеет детейлы D, связанные агрегацией DA. Для A определено [представление](view-definition.html), в которое связано [представление](view-definition.html) детейла D.

Теперь, представим, что выполняется чтение объекта данных типа A по представлению `AView`.  Соответственно, поскольку объекты классов D1, D2 [унаследованы](inheritance.html) от D, они также будут читаться по представлению `DView` (представления наследуются). Однако, что же делать, если они имеют более полный атрибутный состав, который ''обязательно'' нуждается в прочитке?

Для того, чтобы разрешить данную проблему, существуют '''адаптивные''' представления. Если объявить представление `DView` адаптивным, а для детейлов D1 и D2 объявить представления с теми же именами (`DView`), но с собственным атрибутным составом, то [сервис данных](data-service.html) будет прочитывать детейлы D1 и D2 в соответствии с ним.

Для того, чтобы указать, что представление адаптивно, необходимо при ассоциировании детейлового представления в атрибуте `[AssociatedDetailViewAttribute](view-definition.html)` проинициализировать свойство `UseAdaptiveViewsLoading=true`.
Пример:
```
[AssociatedDetailView("AView", "D", "DView", UseAdaptiveViewsLoading=true)]
```
Не следует злоупотреблять адаптивными представлениями, т.к. это негативно влияет на производительность. Во многих случаях лучше отдельно дочитывать детейловые объекты данных.
