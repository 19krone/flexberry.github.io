---
title: Updating related objects
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, DataObject, master, detail
summary: Features of updating children's and master's objects
toc: true
permalink: en/fo_update-related-objects.html
lang: en
---

Возможна ситуация, когда сохранение некоторого [объекта данных](fo_data-object.html) может повлечь сохранение связанных с ним объектов, которые явно не были переданы на сохранение.

## Обновление детейловых объектов вместе с шапкой

Если обновляется объект, имеющий [детейловые объекты](fo_detail-associations-properties.html), то те также обновляются, если это предполагает их [статус](fo_processing-status-condition-load.html).

## Обновление мастеровых объектов вместе с внутренним

Если изменён [мастеровой объект](fd_master-association.html), то при обновлении объекта внутреннего класса обновляется также мастеровой.

Вышеуказанные правила применяются ко всем объектам, находящимся в цепочке изменений. Т.е., например, если есть объект внутреннего класса, у которого есть мастеровой с детейлами, то обновляются все. Важно помнить только, что `попадают только измененные объекты`, т.е., [статус](fo_processing-status-condition-load.html) которых предполагает обновление.