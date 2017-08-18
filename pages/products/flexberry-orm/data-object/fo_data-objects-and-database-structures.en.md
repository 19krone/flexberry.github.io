---
title: Хранение объектных данных в реляционной базе данных
sidebar: flexberry-orm_sidebar
keywords: DataObject (объекты данных), Flexberry ORM, Public
toc: true
permalink: en/fo_data-objects-and-database-structures.html
---

Большинство [сервисов данных](fo_data-service.html) обеспечивают работу с реляционным хранилищем.
Объектные данные [Flexberry ORM](fo_flexberry-orm.html) хранит следующим образом:

* Каждый класс — отдельная таблица. 
* Каждый атрибут — отдельное поле в таблице.
* [Мастеровые связи](fd_master-association.html) — внешние ключи таблицы внутреннего класса.
* [Детейловые связи](fo_detail-associations-properties.html) — внешний ключ детейловой таблицы на агрегатор (шапку).
* [Наследуемый](fo_inheritance.html) класс — отдельная от предка таблица.
* Если у [мастерового класса](fd_master-association.html) есть [наследник](fo_inheritance.html), то на его таблицу должен быть внешний ключ в таблице внутреннего класса.
* Каждая [унаследованная](fo_inheritance.html) таблица хранит все атрибуты всех предков. Таким образом, одному экземпляру класса соответствует одна запись в одной таблице (почему сделано именно так, описано [здесь](fo_inheritance.html)).

