---
title: funcSQL
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, Ограничения
toc: true
permalink: ru/fo_func-s-q-l.html
---
* **Продукт**: [Flexberry ORM](fo_flexberry-o-r-m.html)
* **Компонент**: [Компоненты для фильтрации и ограничения выборки получаемых данных](fo_limitation.html)
* **Программная библиотека**: ICSSoft.STORMNET.FunctionalLanguage.dll.
* **Предназначение**: Общее описание работы функции FuncSQL в построителе [функций ограничения](fo_limit-function.html) [SQLWhereLanguageDef](fo_function-list.html).

FuncSQL - функция в построителе [функций ограничения](fo_limit-function.html) [SQLWhereLanguageDef](fo_function-list.html), позволяющая выполнять вставки SQL.

{% include note.html content="Использовать данную функцию не рекомендуется." %}

Для случая, когда [ExternalLanguageDef](fo_external-lang-def.html) не располагает необходимым набором функций, [ограничение](fo_limit-function.html) можно построить в виде SQL-выражения. Пользоваться данной возможностью рекомендуется крайне осторожно, поскольку переключение типов источников данных в этом случае реализуется сложнее, ошибки выявлять тоже непросто.

Важно понимать, что `funcSQL` может быть частью другой "нормальной" функции, в этом случае необходимо не забывать про скобки снаружи этого SQL-выражения. Скобки при интерпретации сами не ставятся.

## Пример

Следующее выражение

``` csharp
lcs.LimitFunction = ldef.GetFunction(ldef.funcAND,
                ldef.GetFunction(ldef.funcSQL, "\"abc\" = 1"),
                ldef.GetFunction(ldef.funcSQL, "\"def\" = 2")
                );

```

будет интерпретировано следующим образом:

``` sql
WHERE ( "abc" = 1 AND "def" = 2)
```

{% include note.html content="Названия атрибутов необходимо заключать в кавычки, это поможет [Flexberry ORM](fo_flexberry-o-r-m.html) корректно обрабатывать [ограничение](fo_limit-function.html)." %}









