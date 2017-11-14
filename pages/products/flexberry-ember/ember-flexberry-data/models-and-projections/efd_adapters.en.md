---
title: Адаптеры в ember-flexberry приложении
sidebar: ember-flexberry-data_sidebar
keywords: Flexberry Ember
toc: true
permalink: en/efd_adapters.html
folder: products/ember-flexberry-data/models-and-projections/
lang: en
summary: Адаптеры определяют, каким образом происходит обращение к серверу для получения данных в ember-flexberry приложении.
---

## Описание

Отличное описание есть в [документации на официальном сайте](https://guides.emberjs.com/v2.4.0/models/customizing-adapters/).

## Настройка адаптеров в приложении

При генерации приложения `ember-flexberry` создается файл `app/adapters/application.js` со следующим содержанием:
```javascript
import { Projection, Adapter } from 'ember-flexberry-data';
import config from '../config/environment';

export default Adapter.Odata.extend(Projection.AdapterMixin, {
  host: config.APP.backendUrls.api,
});
```

Это адаптер для всего приложения, в котором задается адрес `OData` сервиса.

Если для модели не определено собственного адаптера, используется адаптер приложения.
Что бы для определить адаптер для конкретной модели, необходимо создать адаптер с таким же именем как у модели, сделать это можно командой:

```cmd
ember g adapter my-model
```

В результате выполнения этой команды будет создан файл `app/adapters/my-model.js` со следующим содержанием:

```javascript
import ApplicationAdapter from './application';

export default ApplicationAdapter.extend({
});
```

Для того что бы изменить адрес `OData` сервиса для этой модели, необходимо переопределить свойство `host`, указав в нем новый адрес `OData` сервиса.
