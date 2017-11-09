---
title: Search all attributes
sidebar: ember-flexberry_sidebar
keywords: Flexberry Ember, search, OLV, list
summary: Features of the standard search control for list and master forms (raised by LookUp)
toc: true
permalink: en/ef_search-attributes.html
lang: en
---

## Настройка поиска по всем атрибутам для стандартного списка

Для того чтобы на [списковой форме](ef_object-list-view.html) реализовать возможность поиска по всем атрибутам необходимо:

1. Указать свойства поиска в [шаблоне](ef_template.html) списковой формы.
2. При необходимости переопределить предикаты в [роуте](ef_route.html) списковой формы.

### Настройка шаблона формы

Настройка шаблона формы осуществляется следующим образом:

```hbs
{% raw %}{{flexberry-objectlistview
    // ...
    filters=filters
    applyFilters=(action "applyFilters")
    resetFilters=(action "resetFilters")
    filterButton=true
    filterText=filter
    filterByAnyWord=filterByAnyWord // поиск по некоторым словам
    filterByAllWords=filterByAllWords // поиск по всем словам
    filterByAnyMatch=(action 'filterByAnyMatch')
    // ...
}}{% endraw %}
```

`filterByAnyWord` - в результате будут выданы все строки, в которых указано заданное в поиске слово/несколько слов.

![](/images/pages/products/ember-flexberry/controls/filter-by-any-word.png)

`filterByAllWords` - в результате будут выданы только те строки, в которых указано заданное слово/словосочетание.

![](/images/pages/products/ember-flexberry/controls/filter-by-all-words.png)

По-умолчанию поиск осуществляется по подстроке.

Реализация отображена на [ember-стенде](https://flexberry-ember-dev.firebaseapp.com/)
* [для OLV](https://flexberry-ember-dev.firebaseapp.com/components-examples/flexberry-objectlistview/custom-filter?filterCondition=and&perPage=20).
* [для simpleolv](https://flexberry-ember-dev.firebaseapp.com/components-examples/flexberry-simpleolv/custom-filter)

{% include note.html content="`filterByAnyWord` и `filterByAllWords` нельзя использовать вместе, если не реализованы дополнительные элементы тулбара (кнопки) для включения/отключения типа поиска." %}

### Настройка роута формы

Переопределить, как будет строится предикат, можно следующим образом:

```javascript
predicateForAttribute(attribute, filter) {
    switch (attribute.type) {
      case 'boolean':
        let yes = ['TRUE', 'True', 'true', 'YES', 'Yes', 'yes', 'ДА', 'Да', 'да', '1', '+'];
        let no = ['FALSE', 'False', 'false', 'NO', 'No', 'no', 'НЕТ', 'Нет', 'нет', '0', '-'];

        if (yes.indexOf(filter) > 0) {
          return new SimplePredicate(attribute.name, 'eq', 'true');
        }

        if (no.indexOf(filter) > 0) {
          return new SimplePredicate(attribute.name, 'eq', 'false');
        }

        return null;

      default:
        return this._super(...arguments);
    }
  },
```

Настройка предиката необходима для корректного поиска значений, имеющих два признака истина/ложь.

_Для flexberry-simpleolve настройки аналогичны._

## Настройка списка, отображаемого в лукапе

В [LookUp](ef_lookup.html) показывается компонент [flexberry-objectlistview](ef_object-list-view.html). Параметры для этого компонента можно задавать через событие `getLookupFolvProperties` в контроллере формы:

```javascript
getLookupFolvProperties: function(options) {
    //...

    if (methodArgs.relationName === 'type') {
    return {
        filterButton: true,
        filterByAnyWord: true,
        enableFiltres: true,
        refreshButton: true
      };
    }

    // ...
}
```

{% include note.html content="Необходимо выбрать тип поиска (`filterByAnyWord` или `filterByAllWords`), так на lookup-форме использовать использовать можно только один из них." %}

Далее указать событие в шаблоне настраевомого списка для LookUp:

```hbs
{% raw %}{{flexberry-lookup
    // ...
    lookupWindowCustomProperties=(action 'getLookupFolvProperties')
}}{% endraw %}
```

Реализация отображена на [ember-стенде](https://flexberry-ember-dev.firebaseapp.com/components-examples/flexberry-lookup/customizing-window-example).
