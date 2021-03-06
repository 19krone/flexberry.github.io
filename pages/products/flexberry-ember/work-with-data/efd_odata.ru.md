---
title: Поддержка протокола OData v4
sidebar: flexberry-ember_sidebar
keywords: function, action, callAction, callEmberOdataAction, callFunction, callEmberOdataFunction
toc: true
permalink: ru/efd_odata.html
lang: ru
summary: Компоненты для взаимодействия с backend по протоколу OData.
---

## OData

ember-flexberry-data поддерживает протокол OData v4.

* OData adapter

## Вызов функций и экшенов через Ajax

Для облегчения обращений к функциям и экшенам бэкенда через ajax в OData-адаптере предусмотрены два схожих метода: `callFunction` и `callAction`.

### callFunction

Данный метод предназначен для вызова функций бэкенда. callFunction(functionName, params, url, fields, successCallback, failCallback, alwaysCallback):

* `functionName`: имя функции бэкенда
* `params`: объект, содержащий параметры запроса
* `url`: адрес OData бэкенда. Если не указан – берётся адрес, указанный в `environment.js`
* `fields`: объект вида { имя: значение }, для изменения значений соответствующих полей объекта XMLHttpRequest
* `successCallback`: метод или `Promise`, исполняемые при успешном исполнении запроса
* `failCallback`: метод или `Promise`, исполняемые при неудачном исполнении запроса
* `alwaysCallback`: метод или `Promise`, исполняемые в любом случае.

#### Примеры использования callFunction

* Без callback-функций, URL бэкенда берем из `environment.js`:
```
adapter.callFunction('test', { someParams: 'someParams' })
```
* С callback-функциями:

```
adapter.callFunction(
  'test',
  { someParams: 'someParams' },
  null,
  null,
  () => {
    console.log("This is a successCallback function");
  },
  () => {
    console.log("This is a failCallback function");
  },
  () => {
    console.log("This is an alwaysCallback function");
  }
)
```

### callEmberOdataFunction

Аналогичен методу callFunction, но в качестве результата возвращает эмберные модели. Имеет два дополнительных параметра: store и  modelName. callEmberOdataFunction(functionName, params, url, fields, store, modelName, successCallback, failCallback, alwaysCallback):

* `store`: объект [DS.Store](https://emberjs.com/api/ember-data/release/classes/DS.Store)
* `modelName`: имя эмберной модели

### callAction

Данный метод предназначен для вызова экшенов бэкенда. callAction(actionName, data, url, fields, successCallback, failCallback, alwaysCallback):

* `actionName`: имя экшена бэкенда
* `data`: объект, содержащий параметры запроса
* `url`: адрес OData бэкенда. Если не указан – берётся адрес, указанный в `environment.js`
* `fields`: объект вида { имя: значение }, для изменения значений соответствующих полей объекта XMLHttpRequest
* `successCallback`: метод или `Promise`, исполняемые при успешном исполнении запроса
* `failCallback`: метод или `Promise`, исполняемые при неудачном исполнении запроса
* `alwaysCallback`: метод или `Promise`, исполняемые в любом случае.

#### Примеры использования callAction

* Без callback-функций, URL бэкенда берем из `environment.js`:
```
adapter.callAction('test', { someParams: 'someParams' })
```
* С callback-функциями:

```
adapter.callAction(
  'test',
  { someParams: 'someParams' },
  null,
  null,
  () => {
    console.log("This is a successCallback function");
  },
  () => {
    console.log("This is a failCallback function");
  },
  () => {
    console.log("This is an alwaysCallback function");
  }
)
```

### callEmberOdataAction

Аналогичен методу callAction, но в качестве результата возвращает эмберные модели. Имеет два дополнительных параметра: store и  modelName. callEmberOdataAction(functionName, params, url, fields, store, modelName, successCallback, failCallback, alwaysCallback):

* `store`: объект [DS.Store](https://emberjs.com/api/ember-data/release/classes/DS.Store)
* `modelName`: имя эмберной модели
