---
title: Настройка панели управления (тулбара) во Flexberry Objectlistview (технология Flexberry ASP.NET Ember)
sidebar: ember-flexberry_sidebar
keywords: Flexberry Ember
toc: true
permalink: ru/ef_olv-toolbar.html
folder: product--folder
lang: ru
summary: Представлено, каким образом настраивается панель управления (тулбар) контрола Flexberry Objectlistview.
---

## Описание

Панель управления (тулбар) контрола [Flexberry Objectlistview](ef_objectlistview.html) основана на технологическом контроле `olv-toolbar`.

Настройка панели управления происходит через компонент Flexberry Objectlistview.

## Кнопка создания новой записи

```
`flexberry-objectlistview createNewButton = true ...`
```

`createNewButton` - флаг, определяющий, отображать ли кнопку создания на панели управления.


## Кнопка обновления

```
`flexberry-objectlistview refreshButton = true ...`
```

`refreshButton` - флаг, определяющий, отображать ли кнопку обновления на панели управления.


## Кнопка удаления выделенных записей

```
{{flexberry-objectlistview
	componentName = "..."
	deleteButton = true
	showCheckBoxInRow = true
	...
}}
```

Для того, чтобы начала функционировать кнопка удаления выделенных записей, требуется определить следующие свойства [Flexberry Objectlistview](ef_objectlistview.html):

* `componentName` - имя контрола (используется для идентификации составных частей контрола, которые взаимодействуют через [внедрённый сервис](http://emberjs.com/api/classes/Ember.inject.html#method_service)). Например, в качестве значения для списка записей типа "employee" можно указать "employeesFlexberryObjectListView".
* `deleteButton` - флаг, определяющий, отображать ли кнопку удаления на панели управления.
* `showCheckBoxInRow` - флаг, определяющий, отображать ли чекбоксы в строчках [Flexberry Objectlistview](ef_objectlistview.html).


{% include note.html content="Если в [Flexberry Objectlistview](ef_objectlistview.html) не отмечена ни одна строчка, то кнопка удаления не активна. Когда появляются отмеченные записи, кнопка удаления становится доступна." %}

{% include note.html content="При удалении информация сразу отправляется на сервер для сохранения изменений." %}

## Кнопки пользовательских настроек

При значении атрибута colsConfigButton=true на панели управления (тулбар) отображаются кнопки управления пользовательскими наcтройками.

```hbs
{{flexberry-objectlistview
	componentName = "..."
	colsConfigButton=true
	...
}}
```

Подробно о функционале пользовательских настроек можно почитать на странице [Сервис настроек пользователя](ef_model-user-settings-service.html).

## Добавление пользовательских кнопок на панель управления

На панель управления можно добавлять кнопки, реализующие пользовательскую логику.
Чтобы добавить пользовательскую кнопку, требуется выполнить следующее:

1. В соответствующем прикладном [контроллере](ef_controller.html) определить вычислимое свойство с произвольным именем, например, `сustomButtons`, которое возвращает массив структур вида:

```js
{
 buttonName: '...',
 buttonAction: '...',
 buttonClasses: '...'
}
```

`buttonName` - имя кнопки на интерфейсе пользователя. Если передано пустое значение, то имя кнопки будет 'UserButton'.


`buttonAction` - имя действия (action), которое будет вызываться данной кнопкой (при вызове действия используется [sendAction](http://emberjs.com/api/classes/Ember.Component.html#method_sendAction), поэтому обработчик можно определять как в [контроллере](ef_controller.html), так и в соответствующем [роуте](ef_route.html)). Если передано пустое значение, то в консоли браузера появится сообщение об ошибке. Желательно именовать действия с префиксом "userButtonAction", чтобы случайно не перетереть свойство контрола при регистрации этого действия в контроле.

`buttonClasses` - классы, которые требуется добавить в создаваемую пользовательскую кнопку.

2. В соответствующем прикладном [контроллере](ef_controller.html) (или [роуте](ef_route.html)) определить обработчик события, имя которого было указано в `buttonAction`.

3. В [шаблоне](ef_template.html) соответствующей формы у компонента `flexberry-objectlistview` определить свойства:

```hbs
{{flexberry-objectlistview
  // ...
	customButtons=customButtons
	
	userButtonAction1='userButtonAction1'
	userButtonAction2='userButtonAction2'
	// ...
	userButtonActionN='userButtonActionN'
}}
```

`customButtons` - определение свойства, откуда можно взять массив.


`userButtonAction1`, `userButtonAction2`, ... `userButtonActionN` - регистрация действий, которые определялись в свойстве `buttonAction` ([без такой "регистрации"](http://emberigniter.com/send-action-does-not-fire/) действие может не вызываться и Ember не выдаст сообщения об ошибке).

Рассмотрим данную возможность на примере. Добавим в контрол Flexberry Objectlistview пользовательскую кнопку, которая при клике будет выводить сообщение пользователю.


1. В [шаблоне](ef_template.html) страницы зададим заголовок в виде переменной "header".

```
&lt;h3 class="ui header"&gt;Страница с пользовательскими кнопками&lt;/h3&gt;
&lt;div class="row"&gt;
`flexberry-objectlistview ... `
&lt;/div&gt;
&lt;div class="row"&gt;`messageForUser`&lt;/div&gt;
```

2. В соответствующем прикладном [контроллере](ef_controller.html) определим необходимые переменные, зададим вычислимое локализируемое свойство "customButtons", которое вернёт массив описаний пользовательских кнопок (в данном случае - одной кнопки), зададим действие "userButtonActionTest", которое будет обрабатывать нажатие на кнопку.

```javascript
import Ember from 'ember';
import ListFormController from 'ember-flexberry/controllers/list-form';

export default ListFormController.extend({
  /**
    Property to count clicks on user button.

    @property clickCounter
    @type Number
    @default 1
   */
  clickCounter: 1,

  /**
    Property to show user message after click on user button.

    @property messageForUser
    @type String
   */
  messageForUser: undefined,

  /**
    Property to form array of special structures of custom user buttons.

    @property customButtons
    @type Array
   */
  customButtons: Ember.computed('i18n.locale', function() {
    let i18n = this.get('i18n');
    return [{
      buttonName: i18n.t('forms.components-examples.flexberry-objectlistview.toolbar-custom-buttons-example.custom-button-name'),
      buttonAction: 'userButtonActionTest',
      buttonClasses: 'my-test-user-button test-click-button'
    }];
  }),

  actions: {
    /**
      Handler for click on custom user button.

      @method userButtonActionTest
     */
    userButtonActionTest: function() {
      let i18n = this.get('i18n');
      let clickCounter = this.get('clickCounter');
      this.set('clickCounter', clickCounter + 1);
      this.set('messageForUser',
        i18n.t('forms.components-examples.flexberry-objectlistview.toolbar-custom-buttons-example.custom-message').string +
        ' ' + clickCounter);
    }
  }
});
```

3. В [шаблоне](ef_template.html) укажем свойство для получения пользовательских кнопок, а также зарегистрируем наше пользовательское действие.

```
&lt;h3&gt;`header`&lt;/h3&gt;

&lt;div class="row"&gt;
  {{flexberry-objectlistview
    ...
	customButtons=customButtons
	userButtonActionTest='userButtonActionTest'
  }}
&lt;/div&gt;
```