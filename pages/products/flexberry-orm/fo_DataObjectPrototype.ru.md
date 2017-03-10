---
title: Создание объекта данных на основе другого (прототипизация)
sidebar: flexberry-orm_sidebar
keywords: DataObject (объекты данных), Flexberry ORM, Public
toc: true
permalink: ru/fo_data-object-prototype.html
---
<<<<<<< HEAD
# Методы для прототипизации DataObject
Для прототипизации `[DataObject](fo_dataobject.html)` существует метод `Prototyping`.
=======
## Методы для прототипизации DataObject
Для прототипизации `[DataObject](fo_dataobject.html)` существует метод `Prototyping`.

>>>>>>> d39794c485bf490f825f86803b545b9c10b0808f
```cs
/// <summary>
/// Прототипизировать
/// </summary>
/// <param name="withDetails">с детейлами или без</param>
public virtual void Prototyping(bool withDetails)
```

Также существует перегрузка данного метода без параметров (в этом случае будет просто произведён вызов метода `Prototyping(true)`).

## Прототипизация DataObject
При прототипизации происходят следующие действия:
<<<<<<< HEAD
* сбрасывается значение [первичного ключа объекта](fo_primary-keys-objects.html) (генерируется новое);
* [статус объекта](object-status-and-loading-state.html) изменяется на `ObjectStatus.Created`;
* [состояние загрузки объекта](object-status-and-loading-state.html) устанавливается в `LoadingState.NotLoaded`;
* [вызывается метод `InitDataCopy`](data-object-copy.html).

Если переданный параметр `withDetails` имеет значение `true`, то прототипизация будет выполнена и для всех детейлов.

# Примечания по протитопизации
* Получить [первичный ключ объекта](fo_primary-keys-objects.html), который он имел до прототипизации, можно через свойство `<nowiki>__PrototypeKey</nowiki>`.
* Очистка свойства `<nowiki>__PrototypeKey</nowiki>` происходит при вызове метода `ClearPrototyping` (если вызов был произведён без параметров или значение параметра было `true`, то соответствующее свойство будет очищено и у детейлов).
* Вызов метода `ClearPrototyping(true)` также происходит при сохранении объекта через [SQLDataService](fo_sql-data-service.html).
* Узнать, был ли объект прототипизирован можно через свойство `Prototyped`.
* При выполнении [дочитки объекта](additional-loading-data-object.html) сервис данных будет осуществлять вычитку свойств прототипизированного объекта, используя в качестве [первичного ключа](fo_primary-keys-objects.html) `<nowiki>__PrototypeKey</nowiki>` (но при выполнении UpdateObject в БД будет создан новый объект).
=======

* сбрасывается значение [первичного ключа объекта](fo_primary-keys-objects.html) (генерируется новое);
* [статус объекта](fo_object-status-and-loading-state.html) изменяется на `ObjectStatus.Created`;
* [состояние загрузки объекта](fo_object-status-and-loading-state.html) устанавливается в `LoadingState.NotLoaded`;
* [вызывается метод `InitDataCopy`](fo_data-object-copy.html).

Если переданный параметр `withDetails` имеет значение `true`, то прототипизация будет выполнена и для всех детейлов.

## Примечания по протитопизации
>>>>>>> d39794c485bf490f825f86803b545b9c10b0808f

* Получить [первичный ключ объекта](fo_primary-keys-objects.html), который он имел до прототипизации, можно через свойство `PrototypeKey`.
* Очистка свойства `PrototypeKey` происходит при вызове метода `ClearPrototyping` (если вызов был произведён без параметров или значение параметра было `true`, то соответствующее свойство будет очищено и у детейлов).
* Вызов метода `ClearPrototyping(true)` также происходит при сохранении объекта через [SQLDataService](fo_s-q-l-data-service.html).
* Узнать, был ли объект прототипизирован можно через свойство `Prototyped`.
* При выполнении [дочитки объекта](fo_additional-loading-data-object.html) сервис данных будет осуществлять вычитку свойств прототипизированного объекта, используя в качестве [первичного ключа](fo_primary-keys-objects.html) `PrototypeKey` (но при выполнении UpdateObject в БД будет создан новый объект).
