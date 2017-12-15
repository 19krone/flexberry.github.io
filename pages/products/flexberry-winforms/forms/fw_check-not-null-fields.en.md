---
title: Проверка обязательных полей
sidebar: flexberry-winforms_sidebar
keywords: Windows UI (формы)
summary: Рассказано как использовать DataObjectErrorProvider для проверки обязательности заполнения поля, не являющегося обязательным в модели, примеры
toc: true
permalink: en/fw_check-not-null-fields.html
folder: products/flexberry-winforms/
lang: en
---

Если поля одного класса на одной форме редактирования должны быть обязательно заполнены, а на другой нет, то для отображения и проверки обязательных для заполнения полей (не отмеченных в классе атрибутом [`NotNull`](fo_attributes-class-data.html)) можно воспользоваться [`DataObjectErrorProvider`](fw_data-object-error-provider.html)

## Порядок действий
* кинуть DataObjectErrorProvider на форму
* привязать DataObjectErrorProvider к EditManager (к которому привязаны проверяемые поля)(DataObjectErrorProvider.EditManagerForBind)
* задать проверяемые поля в DataObjectErrorProvider.Properties

```csharp
// 
// dataObjectErrorProvider1
// 
this.dataObjectErrorProvider1.DpdEditContainer = this;
this.dataObjectErrorProvider1.EditManagerForBind = this.EditManager;
this.dataObjectErrorProvider1.Properties = new string[] {
  "НомерКУСП",
  "ТипКарточки",
  "ВремяЗаполнения"};
```


* связать DataObjectErrorProvider с объектом данных. Вызвать dataObjectErrorProvider1.BindToData(); в методе Edit
* для того чтобы отобразить ошибку для поля объекта (таракан), можно воспользоваться BindToData() или SetError() для определенного поля

```csharp
if (obj #  null || obj.ToString()  "")
    dataObjectErrorProvider1.SetError(property, EditManager.NotNullToolTip);
else
    dataObjectErrorProvider1.SetError(property, string.Empty);
```

* добавления полей в сообщение о не заполненности обязательных полей при сохранении. В независимой форме редактирования в методе OnSave() написать:

```csharp
System.Collections.ArrayList arl = new System.Collections.ArrayList();//массив, куда попадут заголовки, из указанного представления, незаполненные полей
arl.AddRange(obj.CheckNotNullProperties(m_objView, true));//обязательные поля объекта (отмеченных в классе атрибутом NotNull)          
string[] s1 = form.dataObjectErrorProvider1.GetNullProperties();//обязательные поля, указанные в dataObjectErrorProvider1
for (int i = 0; i < s1.Length; i++)
   arl.Add(m_objView.GetProperty(s1[i]).Caption);           
if (arl.Count > 0)
{
   form.dataObjectErrorProvider1.FocusFirstNullProperty();//устанавливаем фокус на первое в массиве не заполненное обязательное поле
   IIS.WinUI.Tools.ShowWarning("Остались незаполненными обязательные поля: " + Environment.NewLine + string.Join(", ", (string[])arl.ToArray(typeof(string))), "Внимание");
   ОтменитьСохранение();
   return;
}
```