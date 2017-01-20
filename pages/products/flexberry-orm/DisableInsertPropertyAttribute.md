---
title: DisableInsertPropertyAttribute
sidebar: product--sidebar
keywords: DataObject (объекты данных), Flexberry ORM, Public
toc: true
permalink: ru/disable-insert-property-attribute.html
folder: product--folder
lang: ru
---
Атрибут `DisableInsertPropertyAttribute` позволяет исключить свойство класса из Insert-запросов. Рекомендуется к применению, если есть Default-значение в БД, которое надо применять при создании объекта, либо если БД сама при вставке правильно инициализирует это значение (различные id).

```cs
private int fId = 100;
[DisableInsertPropery(true)]
public virtual int Id
{
	get
	{
		int result = this.fId;
		return result;
	}
	set
	{
		this.fId = value;
	}
}
```
----