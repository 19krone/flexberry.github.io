---
title: DataObjectCopy
sidebar: flexberry-orm_sidebar
keywords: DataObject (объекты данных), Flexberry ORM, Public
toc: true
permalink: ru/fo_data-object-copy.html
folder: products/flexberry-orm/
lang: ru
---

## Копия объекта данных

[Сервис данных](fo_data-service.html) выполняет построение запросов на изменение строк в БД на основе информации об изменённых свойствах объекта. Для получения этой информации в самом [объекте](fo_data-object.html) хранится отдельная полная копия объекта (при этом для выявления изменений требуется лишь сравнить текущие значения полей объекта данных и соответствующих значений в его копии).

Копия объекта данных доступна через метод `dataobject.GetDataCopy()`.

Копия данных заполняется из значений полей объекта в нескольких случаях:

* При вычитке объекта из БД (если не было указано, что инициализировать копию данных не надо).
* При вызове метода `dataobject.InitDataCopy()` программистом.

## Оптимизация работы

Операция создания копии данных - довольно дорогостоящая операция в плане производительности, поэтому рекомендуется при вычитке объектов, которые точно не будут обновляться в БД, отключать инициализацию копии данных в свойствах [LoadingCustomizationStruct](fo_loading-customization-struct.html): 

```csharp
LoadingCustomizationStruct lcs = LoadingCustomizationStruct.GetSimpleStruct(typeof(Шапка), "ШапкаE");
lcs.InitDataCopy = false;
```

Также в целях оптимизации не происходит инициализация мастеровых полей. Для мастеров инициализируются только [первичные ключи](fo_primary-keys-objects.html). Если мастеровой объект был вычитан с достаточным количеством полей и его планируется обновлять в БД, то сразу после зачитки для него необходимо вызвать метод `InitDataCopy()`.

## Копия данных созданного объекта

Если объект имеет [статус `Created`](fo_object-status-and-loading-state.html), то у него отсутствует копия данных после инициализации копии данных (InitDataCopy), поскольку копия данных объекту, у которого [статус `Created`](fo_object-status-and-loading-state.html) не нужна (при обновлении данный объект весь пойдёт в базу, и InitDataCopy пропускает такие объекты).









