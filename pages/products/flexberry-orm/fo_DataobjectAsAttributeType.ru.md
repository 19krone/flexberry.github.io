---
title: Атрибут класса типа объекта данных
sidebar: flexberry-orm_sidebar
keywords: DataObject (объекты данных), Flexberry Designer, Public
toc: true
permalink: ru/fo_dataobject-as-attribute-type.html
---
* **Продукт:** [Flexberry Designer](fd_flexberry-designer.html)
* **Компонент:** [Редактор UML-диаграмм](fd_editing-diagram.html)
* **Предназначение:** Описаны особенности использования [объекта данных](fo_dataobject.html) в виде атрибута класса.

Если на [диаграмме классов](fd_class-diagram.html) нужен [атрибут](fo_attributes-class-data.html) с типом, унаследованным от [DataObject](fo_dataobject.html), нужно:

* сгенерировать и откомпилировать этот тип.
* создать требуемый класс с этим атрибутом, прописать Namespace и полное имя сборки (относительно папки с Flexberry Designer) в которой определён указанный тип.

Только после этого производится генерация такого класса.

![](/images/pages/products/flexberry-orm/data-object-as-attribute-type/data-object-as-attribute-type.GIF)

Использование атрибута класса типа объекта данных не рекомендуется использовать в общем случае, если есть возможность использовать [мастера](fd_master-association.html) или [детейлы](fo_detail-associations-and-their-properties.html).

Основною особенностью данного решения является то, что между классами в таком случае нет связи, в данном случае между классами `Зоопарк` и `ДиректорЗоопарка`. Соответственно, поле `Директор` класса `Зоопарк` будет содержать не ссылку на `ДиректорЗоопарка`, а хранить [сериализованный объект](fo_aggregating-function.html) `ДиректорЗоопарка`.

Применение атрибута класса типа [объекта данных](fo_dataobject.html) может быть полезным при сохранении специализированных настроек, когда возвращается объектная модель настроек, а не просто строка.









