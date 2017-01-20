---
title: Автодополнение в веб системах (AjaxAutocomplete)
sidebar: product--sidebar
keywords: Flexberry ASP-NET, Web UI (Контролы)
toc: true
permalink: ru/ajax-autocomplete.html
folder: product--folder
lang: ru
---

<div style="margin:5px; padding-left:28px; float:right; width:60%; outline:1px solid white;">
<br>
<table border="0" width="100%" bgcolor="#6495ED">
<tbody><tr><td bgcolor="#FFFFFF">
&nbsp;&nbsp;&nbsp;'''AjaxAutocomplete '''

* '''Платформа''': Web.
* '''Предназначение''': контрол, используемый для автозаполнения поля вводимыми ранее значениями. 
* '''JavaScript API:''' 
* '''[Автодокументация](http://storm:20013/class_i_c_s_soft_1_1_s_t_o_r_m_n_e_t_1_1_web_1_1_ajax_controls_1_1_ajax_autocomplete.html)'''.
* '''[AjaxAutocomplete на тестовом стенде](http://ru:6158/forms/Controls/AjaxAuto%D0%A1omplete/)''' .

</td>
</tr></tbody></table></a>
</div>

# Описание
При помощи AjaxAutocomplete вы можете, например, при редактировании имени объекта получить автодополнение для данного поля, в котором будут предлагаться имена существующих объектов, начинающихся на введенные символы.
AjaxAutocomplete используется из библиотеки jquery ui, поэтому библиотека jquery ui должна быть подключена.

Также, имеется возможность связать [автодополнение с лукапом](link--ajax-autocomplete-and--ajax-lookup.html).<br />
Либо включить автодополнение у [Ajax-лукапа](master-editor-ajax-look-up.html).

# Подключение
Если вы используете последнюю версию веб-шаблона, то все необходимые файлы у вас уже имеются, вы можете пропустить этот пункт и перейти к пункту "Использование"

Для того, чтобы добавить поддержку автодополнения, необходимо:
1. Обновить версию `ICSSoft.STORMNET.Web.AjaxControls.dll`
2. Добавить стили `jquery-ui.css` и картинку с индикатором загрузки `indicator.gif`;
3. Добавить библиотеку `jquery ui`;
4. Обновить версию `ICSSoft.STORMNET.Web.Tools.dll`

# Использование
Будьте внимательны при использовании веб-сервиса. Убедитесь, что настройки для [ServiceSecurityProvider](service-security-provider.html) указаны верно.

Для того, чтобы указать контрол, к которому будет применятся авдотополнение, необходимо добавить метод 
```cs
AjaxAutocomplete.AddControlAutocomplete(контрол, тип_объектов, свойство_объекта)
```

например, в `Page_Load()`;

Имеется возможность указать: использовать ли поиск по подстроке и ограничение.

```cs
//AjaxAutocomplete.AddControlAutocomplete(контрол, тип_объектов, свойство_объекта, использовать_ли_поиск_по_подстроке, ограничение);
AjaxAutocomplete.AddControlAutocomplete(ctrlЦена, typeof(Кошка), "Цена", false, func2);
```

## Пример
```cs
AjaxAutocomplete.AddControlAutocomplete(ctrlКличка, typeof(Кошка), "Кличка");
AjaxAutocomplete.AddControlAutocomplete(ctrlЦена, typeof(Кошка), "Цена");
```

## Сортировка и Distinct
Если для ввода указано представление, то все поля попадут под Distinct. Накладывать сортировку можно на любое свойство в представлении.

## Раскраска совпадающих символов в выпадающем списке
Весь javascript, связанный с автодополнением находится в файле `AjaxDataService.js`.

Для раскраски символов был переопределен `renderItem` у прототипа автокомплита.

```javascript
$(function () {
    $.ui.autocomplete.prototype._renderItem = function (ul, item) {
        var re = new RegExp(this.term, 'i');
        var t = item.label.replace(re, "<span style='font-weight:bold;color:Blue;'>" +
            this.term +
                "</span>");
        return $("<li></li>")
            .data("item.autocomplete", item)
            .append("<a>" + t + "</a>")
            .appendTo(ul);
    };
});
```
