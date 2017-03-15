---
title: FuncEQ
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, Ограничения
toc: true
permalink: ru/fo_func-e-q.html
---
* **Продукт**: [Flexberry ORM](fo_flexberry-o-r-m.html)
* **Компонент**: [Компоненты для фильтрации и ограничения выборки получаемых данных](fo_limitation.html)
* **Программная библиотека**: ICSSoft.STORMNET.FunctionalLanguage.dll.
* **Предназначение**: Общее описание работы функции FuncEQ в построителе [функций ограничения](fo_limit-function.html) [SQLWhereLanguageDef](fo_function-list.html).

FuncEQ - функция, аналогичная сравнению на равенство в SQL, в построителе [функций ограничения](fo_limit-function.html) [SQLWhereLanguageDef](fo_function-list.html).

## Параметры GetFunction

Функция [GetFunction](fo_function-list.html) принимает первым параметром тип функции funcEQ, а дальше принимает 2 объекта на сравнение их между собой. Первым посылается описание переменной (Variable Definition), по которому будут определяться объекты для сравнения; а вторым параметром - объект, с которым будет происходить сравнение.

**Исключение** составляет тип `bool`: `langdef.GetFunction(langdef.funcEQ, new VariableDef(langdef.BoolType, "SomeBoolFlag"))` сработает и без указания второго параметра (по умолчанию будет происходить сравнение с `true`).

**Проверку на `null`** надо проводить при помощи функции [FuncIsNull), при попытке проверить что-либо на `null` с помощью FuncEQ возникнет исключительная ситуация **Object reference not set to an instance of an object.**

## Пример использования

Рассмотрим пример. Требуется вычитать все **Кредиты** определенного **Клиента**.

![](/images/pages/products/flexberry-orm/func-e-q/FilterExDiagram.PNG)

SQL-выражение выглядело бы следующим образом:

```sql
SELECT * FROM Кредит WHERE Клиент = '{ID}'@@
Где {ID} - [Primary-keys-objects|первичный ключ) искомого `Клиента`
```

Через [SQLWhereLanguageDef](fo_function-list.html):

```cs   
Клиент клиент = new Клиент();
SQLWhereLanguageDef langdef = SQLWhereLanguageDef.LanguageDef;
Function lf = langdef.GetFunction(langdef.funcEQ, new VariableDef(langdef.GuidType, Information.ExtractPropertyPath<Кредит>(x => x.Клиент)), клиент.__PrimaryKey);
```

## Особенности сравнения строк

{% include important.html content="При использовании [MS SQL DataService](fo_mssql-data-service.html) могут возникать [проблеммы со сравнением строк с пробелами на конце](http://improvingsoftware.com/2009/09/09/beware-of-this-trap-when-comparing-strings-in-t-sql-with-trailing-spaces/)." %}

Дело в том, что MS SQL Sever следует стандарту [ANSI SQL-92](https://ru.wikipedia.org/wiki/SQL-92) в том, что касается сравнения строк.

Чтобы определить, равны ли строки неодинаковой длины, прежде всего с правой стороны более короткой строки добавляются пробелы, так что длины строк становятся равными.

Затем символы в первой строке сравниваются с символами второй с учетом их расположения. Если не равна хотя бы одна пара, строки считаются неравными.

Это касается сравнений типа WHERE strfield = '...', или HAVING strfield='...', или strfield IN ('...', '...', ...). В этих случаях строки 'abc' и 'abc  ' будут считаться равными.

Исключением является оператор LIKE (WHERE strfield LIKE '...'), для него строки 'abc' и 'abc  ' - различны, поэтому для наложения ограничений на строки следует использовать функцию [funcLike](fo_func-like.html).
