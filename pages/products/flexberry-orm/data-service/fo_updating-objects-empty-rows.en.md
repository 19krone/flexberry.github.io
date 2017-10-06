---
title: Updating objects with empty rows
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, data service, mssql, empty string
summary: Using MSSQLDataService when updating objects with empty strings
toc: true
permalink: en/fo_updating-objects-empty-rows.html
lang: en
---

[MSSQLDataService](fo_mssql-data-service.html) преобразует пустые строки в `NULL` при обновлении объектов.

При построении [ограничения](fo_limitation.html), если параметром в проверке на равенство передаётся `String.Empty`, то запрос будет сгенерирован как IS NULL и всё сработает так как надо. Это упрощение избавляет от необходимости писать сложные Where-выражения.

Если есть потребность различать `NULL` и `String.Empty`, то можно [унаследоваться от MSSQLDataService и переопределить метод](fo_implement-custom-ds.html) 

``` csharp
public virtual string ConvertSimpleValueToQueryValueString(object value)
``` 
таким образом, чтобы не выполнялась замена 

``` csharp
if (valType == typeof(string))
{
	if ((string)value == string.Empty)
		return "NULL";
	else
		return "'" + value.ToString().Replace("'", "''") + "'";
}
```

Особое внимание следует обратить на эту особенность, если используются импортированные данные или SQL-выражения, которые выполняются в обход [сервиса данных](fo_data-service.html).
