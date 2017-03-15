---
title: FuncNEQ
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, Ограничения
toc: true
permalink: ru/fo_func-n-e-q.html
---
* **Продукт**: [Flexberry ORM](fo_flexberry-o-r-m.html)
* **Компонент**: [Компоненты для фильтрации и ограничения выборки получаемых данных](fo_limitation.html)
* **Программная библиотека**: ICSSoft.STORMNET.FunctionalLanguage.dll.
* **Предназначение**: Общее описание работы функции FuncNEQ в построителе [функций ограничения](fo_limit-function.html) [SQLWhereLanguageDef](fo_function-list.html).

FuncNEQ = Not Equal

Функция, аналогичная неравенству в SQL.

## Пример
Рассмотрим пример

![](/images/pages/products/flexberry-orm/func-e-q/FilterExDiagram.PNG)

## Задача

Вычитать все `Кредиты`, не относящиеся к определенному `Клиенту`.

## SQL

SQL-выражение выглядело бы следующим образом:

```sql
SELECT * FROM Кредит WHERE Клиент <> '{ID}'
```

Где {ID} - [первичный ключ](fo_primary-keys-objects.html) `Клиента`


## [FunctionalLanguage](fo_function-list.html)

```cs    
	Клиент клиент = new Клиент();
	SQLWhereLanguageDef langdef = SQLWhereLanguageDef.LanguageDef;
	Function lf = langdef.GetFunction(langdef.funcNEQ,
				new VariableDef(langdef.GuidType, "Клиент"), клиент.__PrimaryKey);
```


## Параметры GetFunction

Из примера видно, что функция GetFunction принимает первым параметром тип функции funcNEQ, а дальше принимает 2 объекта на сравнение их между собой. Первым посылается описание переменной (Variable Definition), по которому будут определяться объекты для сравнения; а вторым параметром - объект, с которым будет происходить сравнение.

**Примечание**: несмотря на то, что при построении ограничения на переменную типа `bool` [FuncEQ](func-e-q.html) позволяет не посылать второй параметр, FuncNEQ не позволяет этого сделать. Таким образом 

```cs
 langdef.GetFunction(langdef.funcNEQ, new VariableDef(langdef.BoolType, "SomeBoolFlag")) 
``` 

выдаст ошибку.


## Пример

```cs
SQLWhereLanguageDef langdef = SQLWhereLanguageDef.LanguageDef;

LoadingCustomizationStruct lcs = LoadingCustomizationStruct.GetSimpleStruct(typeof(Кредит), Кредит.Views.КредитE);	
Function lf = langdef.GetFunction(langdef.funcNEQ, 
new VariableDef(langdef.GuidType, "Клиент"), клиент.__PrimaryKey);
lcs.LimitFunction = lf;

var credits = DataServiceProvider.DataService.LoadObjects(lcs);
```


## См. также

[Перечень функций](fo_function-list.html)

[FuncEQ](func-e-q.html)


