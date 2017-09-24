---
title: Помещение списка объектов в ObjectListView
sidebar: flexberry-winforms_sidebar
keywords: DataObject (объекты данных), Windows UI (Контролы)
toc: true
permalink: ru/fw_put-list-objects-in--object-list-view.html
folder: products/flexberry-winforms/
lang: ru
---

# Имеется список объектов, которые были созданы не из базы, а прямо в коде. Как этот список отобразить в [ObjectListView](object-list-view.html)?

# ObjectListView

Так как `ObjectListView` не используется для отображения данных не из базы, стандартного способа отобразить список объектв, созданных прямо в коде, нет.

Однако, отобразить данные "из кода" вполне реально.

# Алгоритм добавления данных

# Создать список данных, которые будут отображены.
# Установить у OLV'а используемый тип и представление.
# Установить `LimitFunction` так, чтобы из базы ничего не подгрузилось.
# Вызвать метод `SetObjects`.

## Создание списка данных
Просто создаем список данных, которые необходимо будет загрузить в OLV. Не обязательно, чтобы эти данные были в базе.

Предположим, что мы создаем список объектов и сохраняем его в переменную `myObjects`.


## Установка используемого типа и представления
Предположим, что мы хотим отображать объекты типа `Адрес`, по представлению `АдресL`.

В коде установить настройки OLV'а:

```
objectListView1.DataObjectTypes = new[] { typeof(Адрес) };
objectListView1.ViewName = "АдресL";```
(((<msg type=Important>Несмотря на то, что данные не обязательно должны находиться в базе, представления у класса, отвечающего за эти данные '''должно быть'''</msg>)))


## Блокировка подгрузки данных из базы
Чтобы данные из базы не подгружались во время обновления (нажатия на кнопку Refresh), необходимо установить LimitFunction у OLV'а так, чтобы условие никогда не выполнялось. Вполне подойдет следующий вариант:

```
SQLWhereLanguageDef langdef = SQLWhereLanguageDef.LanguageDef;
objectListView1.LimitFunction = langdef.GetFunction(langdef.funcSQL, "1 = 2");```

(((<msg type=note>В качестве функции-блокироватора можно использовать все что угодно, на ваш вкус и фантазию.</msg>)))

## Непосредственно добавление объектов в список
Чтобы добавить объекты в список достаточно вызвать метод `SetObjects` у OLV'a:

```
objectListView1.SetObjects(myObjects.ToArray());
```

Однако, если вызвать этот метод в момент создания формы, то данные потеряются при нажатии на кнопку `Refresh`.

Чтобы данные сохранялись, необходимо вызывать этот метод после загрузки данных из базы. Для этого, необходимо подписаться на событие `AfterFillData` и добавить в обработчик вызов метода `SetObjects`, к примеру так:

```
objectListView1.AfterFillData += (o, s) =>
{
	objectListView1.SetObjects(myObjects.ToArray());
};
```