---
title: Модули расширения функциональности Flexberry Designer
sidebar: flexberry-designer_sidebar
keywords: CASE Plugins, Flexberry Designer, Public
toc: true
permalink: ru/fd_case-plugins.html
folder: products/flexberry-designer/about/
lang: ru
---

Модули расширения добавляют функциональность во [Flexberry Designer](fd_flexberry-designer.html), предоставляя новые возможности. Модулем может быть генератор исходного кода, утилита поиска, импорта-экспорта и т.п.

При использовании модулей расширения появляются дополнительные пункты меню при выборе репозитарных объектов Flexberry Designer: [Конфигурации, Стадии или Системы](fd_recommended-structure-repository-and-placing-diagrams.html).

Модули хранятся в библиотеках (DLL) и располагаются в папке с исполняемым файлом `Flexberry Designer`.

## Подключение модуля

Перед использованием модулей, их следует подключить к `Flexberry Designer`:
1. Зарегистрировать модули в базе, в которой хранятся репозитарии моделей;
2. Для конкретного репозитария (или Проекта, или Конфигурации, или Стадии) выбрать из зарегистрированных модулей, с которыми ведётся работа в рамках соответствующего репозитария (Проекта, Конфигурации или Стадии).

### Регистрация модулей в базе репозитариев

1.  Выберать в меню пункт Настройки\Модули:

![](/images/pages/products/flexberry-designer/about/pluginsreg.png)

2. Нажать кнопку `Создать` в панели инструментов списка модулей:

![](/images/pages/products/flexberry-designer/about/addplugin.png)

3. Выбрать модуль - динамически подключаемую библиотеку (*.dll), где расположен модуль;
4. Повторить с пункта 2, если нужно зарегистрировать несколько модулей.

### Выбор модуля для репозитария, проекта, конфигурации или стадии

1.  Открыть форму редактирования свойств репозитария, проекта, конфигурации или стадии:

![](/images/pages/products/flexberry-designer/about/editrepprop.png)

2. Выбрать необходимые модули:

![](/images/pages/products/flexberry-designer/about/propeditselectmodules.png)

3. Надать в панели инструментов кнопку Сохранить.
4. Модули подключены.

## Стандартные модули Flexberry Designer
* [Модуль расширения Flexberry ORM](fo_flexberry-orm-case-plugin.html)

## Как реализовать свой модуль расширения Flexberry Designer
[Как создать свой модуль расширения для Flexberry Designer описывается в отдельной статье.](fd_plugins-development.html)
