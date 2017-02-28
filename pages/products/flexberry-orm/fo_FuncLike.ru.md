---
title: FuncLike
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, Ограничения
toc: true
permalink: ru/fo_func-like.html
---
##FuncLike
FuncLike - функция, аналогичная проверке на вхождение подстроки в другую строку в SQL, в построителе функций ограничения SQLWhereLanguageDef.

##Параметры GetFunction
Функция GetFunction принимает первым параметром тип функции funcLike, а дальше принимает 2 объекта на сравнение их между собой. Первым посылается описание переменной (Variable Definition), по которому будут определяться объекты для сравнения; а вторым параметром - маска, с которой будет происходить сравнение.

Рассмотрим пример. Требуется вычитать всех Клиентов с пропиской в городе Перми. (Для упрощения задачи, будем считать достаточным наличия слова "Пермь" в строке Клиент.Прописка)

SQL-выражение выглядело бы следующим образом:

```
SELECT * FROM Клиент WHERE Прописка like '%Пермь%'
```

Через SQLWhereLanguageDef:

```
SQLWhereLanguageDef langdef = SQLWhereLanguageDef.LanguageDef;
Function lf = langdef.GetFunction(
            langdef.funcLike,
            new VariableDef(langdef.StringType, Information.ExtractPropertyPath<Клиент>(x => x.Прописка)),
            "%Пермь%");
```


