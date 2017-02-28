---
title: FuncBETWEEN
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, Ограничения
toc: true
permalink: ru/fo_func-between.html
---
##funcBETWEEN
FuncBETWEEN - функция, аналогичная проверке на попадание элемента в диапазон значений в SQL, в построителе функций ограничения SQLWhereLanguageDef.

###Параметры GetFunction
Функция GetFunction принимает первым параметром тип функции funcBETWEEN, а дальше принимает 3 параметра. Первым посылается описание переменной (Variable Definition), по которому будут определяться объекты для сравнения; а вторым и третьим - границы диапазона.

Рассмотрим пример. Требуется вычитать все Кредиты, сумма которых находится в диапазоне от 50000 рублей до 75000 рублей.

SQL-выражение выглядело бы следующим образом:

```
SELECT * FROM Клиент WHERE СуммаКредита BETWEEN 50000 AND 75000
```

Через SQLWhereLanguageDef:

```
SQLWhereLanguageDef langdef = SQLWhereLanguageDef.LanguageDef;
Function lf = langdef.GetFunction(langdef.funcBETWEEN,
            new VariableDef(langdef.StringType, Information.ExtractPropertyPath<Кредит>(x => x.СуммаКредита)),
                            50000,
                            75000);
```


