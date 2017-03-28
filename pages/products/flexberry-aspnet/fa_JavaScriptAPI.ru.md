---
title: JavaScript API
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET, JavaScript API
toc: true
permalink: ru/fa_java-script-api.html
folder: products/flexberry-aspnet/
lang: ru
---

# JS API
JavaScript API основано на библиотеке jQuery и представляет собой набор плагинов для неё.
 	
Всю систему клиентского JS API можно разделить на несколько основны групп.
 	
1.`ядро API` (общий набор методов и данных для работы с Flexberry ASP.NET).
* [jquery.ics.js](fa_js-api-core.html)


2.`API контролов` (набор операций для работы с основными технологическими web-контролами).
* [JSAPIWOLV|jquery.icsWolv.js)
* [jquery.ajaxgroupedit.js](fa_ajax-group-edit.html)
* [jquery.icsDatePicker.js](fa_date-picker.html)
* [jquery.icsMasterEditorAjaxDropDown.js](fa_master-editor-ajax-dropdown.html)
* [MasterEditorAjaxLookUp|jquery.icsMasterEditorAjaxLookup.js)

3.`API форм` (набор операций для работы с основными технологическими web-формами).
* `[WebEditForm|jQuery.icsEditForm)`


# Конвенция именования

Имена всех файлов JS API должны соответствовать формату `jquery.icsName.js`, где `Name` - имя плагина JS API.

Если у плагина имеются стилевые CSS файлы, то они должны называться аналогично: `jquery.icsName.css`.
