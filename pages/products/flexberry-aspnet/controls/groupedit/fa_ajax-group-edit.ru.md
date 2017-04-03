---
title: AjaxGroupEdit
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET, JavaScript API, Web UI (Контролы)
toc: true
permalink: ru/fa_ajax-group-edit.html
folder: products/flexberry-aspnet/
lang: ru
---

## Описание

`AjaxGroupEdit`- контрол, который позволяет редактировать множество объектов. Является аналогом [GroupEdit](fw_group-edit.html), для Web-приложений.

## Настройка внешнего вида контрола


### Настройка внешнего вида таблиц в теме Crimea
В тему Crimea были добвлены 2 варианта раскраски таблиц.

По умолчанию используется новый стиль с вертикальной зеброй, для того чтобы изменить раскраску на стандартную нужно в `_VariablesBasic.less` изменить значение переменной `@CrimeaTableStyle` на false.

{% include important.html content="При этом, также измениться и стиль таблиц WOLV" %}

### Настройка контролов внутри AGE

Настройка контролов внутри AGE описана в [статье Настройка контролов внутри AGE](fa_controls-age.html).

### CSS-классы AGE

Описание CSS-классов AGE можно прочистить в [статье CSS-классы AjaxGroupEdit](fa_age-css.html).

### Операции

Описание операций AGE можно прочесть в [статье Операции AjaxGroupEdit](fa_age-operations.html).

### События

Описание событий AGE можно прочитать в [статье События AjaxGroupEdit](fa_age-events.html).

### Добавление объектов в AGE при инициализации формы (новый объект)

Описание алгоритма добавление можно прочитать в [статье Добавление объектов в AGE при инициализации формы (новый объект)](fa_add-objects-age-initialization.html).

### Показ HTML значений

Для того, чтобы корректно показывать HTML значения в ячейках, нужно для атрибута проставить атрибут

```
[IsHTML()|IsHTML()]
```

Т.е. аналогично [HTML в AjaxLookup](fa_master-editor-ajax-lookup.html) и [WOLV](fa_web-object-list-view.html).


### Order-атрибуты

Если в представлении есть order атрибут, то AjaxGroupEdit сбросит сортировку и наложит сортировку по этому атрибуту. В тулбар добавятся 2 кнопки для перемещения строк "вверх" и "вниз", которые уменьшают\увеличивают значение order-атрибута.

{% include warning.html content="Атрибут `Order` выставляется через Flexberry или добавляется вручную в код:

```
[Order()]
```

Атрибут Order применим только к полям типа `int`." %}

### Группировка

Описание алгоритма настройки группировки описано в [статье Настройка группировки в AjaxGroupEdit](fa_grouping-age.html).

### Включение режима Read-only для отдельных столбцов

Описание алгоритма настройки режима Read-only для отдельных столбцов описано в [статье Включение режима Read-only для отдельных столбцов AGE](fa_read-only-age.html).

### Добавление нового объекта

Для создания объекта в WGE имеется последняя строчка для ввода данных. Для того, чтобы ее совсем скрыть нужно указать не только `Add = false`, но и `PlusInRow = false

```csharp
ctrlMyWebGroupEdit.Operations.Add = false;
ctrlMyWebGroupEdit.Operations.PlusInRow = false;
```

## JavaScript API

Для манипуляций с AGE на стороне клиента следует использовать AGE JS API, который представляет собой jQuery плагин (ajaxgroupedit).

### Методы

| Наименование | Параметры | Описание|
|:---------------------|:-------------------|:----------------------------------------------|
| `getDataRows`| `selector`| Метод, возвращающий все `tr`, исключая удаленные. Если `selector` принимает значение "all", то удаленные строки исключены не будут.|
| `addNewRow` | `ИмяПараметра1` - описание назначения | Создание новой строки редактирования.|
| `updateVisualState`| `$container`/ `statusValue`| Метод, проставляющий "звёздочку" для отредактированных значений и прячущий удалённые.|
| `addDependedLookups`| `settings`| Добавление зависимых лукапов (подробнее см. ниже).|
| `deleteRows`| `rows` - jQuery-объект или массив HtmlElement, соответствующий удаляемым строкам | Удаление указанных строк.|
| `deleteAllRows`| | Удаление всех строк.|

### Примеры использования

#### Добавление новой строки

```javascript
 $('#<%=ctrlКомната.ClientID %>').ajaxgroupedit('addNewRow');
```

#### Удаление всех строк

```javascript
<script type="text/javascript">
    $(document).ready(function () {
        $('span#delAllRows').click(function () {
            $('#<%= ctrlКвартира.ClientID %>').ajaxgroupedit('deleteAllRows');
        });
    });
</script>
```

#### Подсчет количества строк

Используем метод `getDataRows`:

```javascript
<script type="text/javascript">
    function getRows() {
        var data = $('#<%=ctrlПодзадача.ClientID%>').ajaxgroupedit('getDataRows');
        if (data.length != 0) {
            var result = '';
            $.each(data, function(index, value) {
                result += value.innerHTML;
            });
            alert('Записей в списке: ' + data.length + '\n' + result);
        } else {
            alert('В списке нет записей.');
        }
    };
</script>
```

### Зависимые лукапы внутри AGE

Для реализации зависимых лукапов есть метод `addDependedLookups`:

```javascript
<script type="text/javascript">
    $(function () {
        $('#<%=ctrlTestLookUpD.ClientID%>').ajaxgroupedit('addDependedLookups', {
            master: '<%=ICSSoft.STORMNET.Information.ExtractPropertyName<WebFormsTestStand.TestLookUpD>(x=>x.TestLookUpA1)%>',
            depended: '<%=ICSSoft.STORMNET.Information.ExtractPropertyName<WebFormsTestStand.TestLookUpD>(x=>x.TestLookUpA2)%>',
            url: '~/Forms/Controls/AjaxGroupEdit/JavaScriptApiTests/TestLinkedLookUpInAGE.aspx',
            method: 'GetPageMethod'
        });
    });
</script>
```

Здесь:

* `master` - название свойства, которое отвечает за мастеровой лукап
* `depended` - название свойства, которое отвечает за зависимый лукап
* `url` - url сервиса, к которому будут идти запросы при смене значения в мастеровом лукапе
* `method` - метод сервиса, к которому будут идти запросы при смене значения в мастеровом лукапе

Пример [зависимых лукапов](fa_change-lcs-lookup-age.html).

## Возможные ошибки

* Не сохраняются изменения (например, добавленные объекты):
    * Убедитесь, что на странице нет js ошибок;
    * Проверьте, вызывается ли метод сохранения в AGE, который хранится в document.WgeSaveHandlers.

Например, по-умолчанию вызов происходит в masterpage.js:

```javascript
if (typeof document.WgeSaveHandlers !== 'undefined') {
  var resHandler;
  $.each(document.WgeSaveHandlers, function (i, handler) {
    resHandler = handler();
    if (resHandler == false) {
      good = false;
      return;
    }
  });
}
```

## Пользовательские настройки
Описание настроек содержится в [статье Пользовательские настройки AjaxGroupEdit](fa_age-user-settings.html).

## Настройки для LookUp
С описанием настроек можно ознакомиться в [статье](fa_settings-lookup-age.html).

## Встраивание прикладных контролов
Информацию о встраивании прикладных контролов можно прочитать в [статье](a-g-e-applied-controls.html).

## Множественный LookUp в AGE
Информацию о множественных LookUp'ах можно прочитать в [статье](multi-look-up-in-a-g-e.html).
