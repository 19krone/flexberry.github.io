---
title: Create a class diagram for the database
sidebar:  flexberry-orm_sidebar
keywords: Flexberry Designer, Flexberry ORM, example, database
summary: Algorithm for creating diagrams on the basis of an example
toc: true
permalink: en/fo_reverse-data-base.html
lang: en
---

[Flexberry Designer](fd_landing_page.html) позволяет создавать диаграммы классов по базе данных для:

* MS SQL Server,
* ORACLE,
* PostgreSQL.

Применение данной функции будет проиллюстрировано на примере БД MS SQL Server. Для Oracle и Postgre SQL операция выполняется аналогично с выбором пунктов меню, соответствующих СУБД.

## Использование

Для того чтобы создать диаграммы по базе данных следует:

* Создать новую Стадию.
* Выделить Стадию, зайти в [ORM -> SQL](fd_configure-ms-sql-generator.html), указать путь к базе данных.
* Создать новый System в этой Стадии.
* Выделить System, выбрать в меню [ORM -> Построить диаграммы по БД -> Microsoft SQL Server](fo_orm-case-plugin.html).

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reengineering-plugin.png)

* Дождаться выполнения операции.

{% include note.html content="При создании диаграмм по базе данных все [детейловые](fo_detail-associations-properties.html) связи будут интерпретироваться как [Ассоциации](fd_master-association.html) 1 - * (это связано с тем, что на уровне БД нет разницы между мастеровыми и детейловыми связями)." %}

При создании диаграммы стандартным образом обрабатываются типы параметров, которые были указанны по умолчанию [в карте типов SQL](fd_types-map.html).

__Например:__ тип `VARCHAR(255)` есть по умолчанию в карте типов SQL, поэтому будет преобразован на диаграмме классов в `string`. Однако в этой карте нет типа `VARCHAR(25)`, поэтому будет создан [typedef](fd_typedef.html) `VARCHAR25`, который в карте типов SQL будет замаппирован на `VARCHAR(25)`, а в карте генератора C#-кода - на `string`.

Также для особой обработки типов параметров возможно добавить их в соответствующие карты типов C# и SQL `перед` созданием диаграммы классов по БД."

## Пример создания диаграммы классов по базе данных

* Создать диаграмму классов, на основе которой будет создана база:

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-7-0.png)

* Выделить стадию и указать путь к базе данных (в данном случае будет использоваться база с именем A-Test-DB).
* Сгенерировать скрипт изменения базы данных:

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-3.png)

и применить его на A-Test-DB.
* Создать стадию для генерации диаграммы классов по базе данных, указать путь к базе A-Test-DB.
* Создать объект System.
* Выделить объект System и сгенерировать диаграмму:

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reengineering-plugin.png)

* Проверить результат: должны быть созданы 4 диаграммы классов

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-7-1.png)

`Reverse:`

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-7-2.png)

`Reverse Object1:`

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-7-3.png)

`Reverse Object2:`

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-7-4.png)

`Reverse Object3:`

![](/images/pages/products/flexberry-orm/module-flexberry-designer/reeng-step-7-5.png)
