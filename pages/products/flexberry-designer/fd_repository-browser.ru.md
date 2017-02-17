---
title: Браузер репозиториев
sidebar: flexberry-designer_sidebar
keywords: Flexberry Designer, Public
toc: true
permalink: ru/fd_repository-browser.html
folder: products/flexberry-designer/
lang: ru
---

## Назначение и структура

Репозиторий является универсальным хранилищем информации о моделях. Специальный браузер обеспечивает доступ к [структуре и элементам репозитория](recommended-structure-repository-and--placing-diagrams.html).

На иллюстрации представлен внешний вид браузера:

![](/images/pages/products/flexberry-designer/diagram/repository-browser.png)

В левой части отображается [структура репозитория по уровням](recommended-structure-repository-and-placing-diagrams.html), в правой - содержимое выбранного в левой части уровня.

Репозиторий представляет собой хранилище всей информации о моделях. Информация в репозитории хранится в [иерархическом виде](recommended-structure-repository-and-placing-diagrams.html).

## Пользовательский интерфейс

Поле "Размещение" показывает текущий путь внутри репозитория.

Назначение кнопок панели инструментов браузера.

![](/images/pages/products/flexberry-designer/diagram/repbrowsertoolbar.jpg)

## Создание/удаление уровней репозитория

* Для создания нового объекта (проекта, конфигурации, фазы, системы) необходимо перейти на соответствующий уровень в браузере (например, для создания системы необходимо перейти на уровень фазы) и нажать кнопку ![](/images/pages/products/flexberry-designer/diagram/newbtn.jpg). В появившемся окне необходимо ввести имя и описание создаваемого объекта.
* Для переименования или редактирования свойств уровня, необходимо выбрать его мышкой и нажать кнопку редактирования свойств объекта ![](/images/pages/products/flexberry-designer/diagram/propertiesbtn.jpg). 
В появившемся окне отредактируйте свойства.
* Для удаления объекта необходимо выбрать его мышкой в правой половине окна браузера и нажать кнопку ![](/images/pages/products/flexberry-designer/diagram/delbtn.jpg).

### Горячие клавиши
Нажатие этих клавиш, при выделенной строке уровня вызовет следующее действие:

* **Enter** - переход на уровень ниже;
* **F2** - открытие редактирования свойств выделенного уровня. Аналогично нажатию ![](/images/pages/products/flexberry-designer/diagram/propertiesbtn.jpg);
* **Delete** - удаление объекта. Аналогично нажатию ![](/images/pages/products/flexberry-designer/diagram/delbtn.jpg).

{% include note.html content="Горячие клавиши работают только в центральном окне (в списке слева не работают)." %}

## Дополнительные возможности браузера репозитариев

* [Ярлыки для диаграмм в Flexberry Designer](flexberry-designer-diagram-links.html)
* [Импорт стадий и диаграмм](import-crp-csdg.html)
* [Работа с диаграммами в браузере репозитория](working-with-diagrams-in-the-repository-browser.html)
