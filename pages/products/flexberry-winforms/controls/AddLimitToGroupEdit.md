---
title: Наложение ограничений на GroupEdit
sidebar: product--sidebar
keywords: Windows UI (Контролы)
toc: true
permalink: ru/add-limit-to-group-edit.html
folder: product--folder
lang: ru
---
# Делегат скрытия строк в GroupEdit
Для наложения простых ограничений на записи, отображаемые в [GroupEdit](group-edit.html), можно воспользоваться делегатом скрытия строк соответствующего контрола. Данный делегат определяет видимость каждой записи в [GroupEdit](group-edit.html).
```cs
public IsObjectVisibleDelegate IsObjectVisible;
public delegate bool IsObjectVisibleDelegate(DataObject dataObject);
```
# Пример использования делегата скрытия строк
Пусть на форме имеется [GroupEdit](group-edit.html) `geВизитКлиентаВБанк`, содержащий записи типа `ВизитКлиентаВБанк`, и в `geВизитКлиентаВБанк` необходимо отобразить только те записи, что содержат пустое значение в поле `ЦельВизита`.

Для решения данной задачи выполним следующее:

1. Определим требуемый делегат (он возвращает `true`, если поле `ЦельВизита` у поданной на вход записи типа `ВизитКлиентаВБанк` не заполнено):
```cs
private bool IsObjectVisibleMyImplement(DataObject dataObject)
{
	return string.IsNullOrEmpty(((ВизитКлиентаВБанк)dataObject).ЦельВизита);
}
```
2. Назначим делегат `geВизитКлиентаВБанк`:
```cs
public class WinformБанкE : ICSSoft.STORMNET.UI.BaseWinEdit, IIS.LookUpEditManager2.DPDIБанкE
{
	//...
	public WinformБанкE()
	{
		//...
		this.geВизитКлиентаВБанк.IsObjectVisible = IsObjectVisibleMyImplement;
		//...
	}
}
```