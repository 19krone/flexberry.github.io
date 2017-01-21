---
title: Настройка контрола фильтрации в WebObjectListView
sidebar: flexberry-aspnet_sidebar
keywords: 
toc: true
permalink: ru/fa_tune-control-delegate-method.html
folder: products/flexberry-aspnet/
lang: ru
---

# Делегат изменения контрола фильтрации
В версии шаблона после 10.11.2014 стал доступен делегат изменения контрола [фильтрации](w-o-l-v-filters.html) (на настоящий момент изменение доступно для [DatePicker](date-picker.html)) в [WebObjectListView](web-object-list-view.html). 

Как работает делегат: модуль фильтрации создаёт контролы для фильтрации посредством [WebControlProvider](web-control-provider.html), где вызывается делегат.

```cs
namespace ICSSoft.STORMNET.Web.Tools
{
    public class WebControlProvider
    {
        /// <summary>
        /// Делегат, позволяющий донастраивать контрол после его создания.
        /// </summary>
        public TuneControlDelegate TuneControlDelegateMethod;
		
		...
    }
}
```
## CreatedControlData
`CreatedControlData` - это особая структура, сообщающая в делегат, откуда и для чего был создан контрол (выложена версия с описанием от 10.11.2014, планируется расширять перечисление `CreateControlReason`):
```cs
namespace ICSSoft.STORMNET.Web.Tools
{
    public class CreatedControlData
    {
	
		...
	
        /// <summary>
        /// Список вариантов причин создания контролов.
        /// </summary>
        public enum CreateControlReason
        {
            /// <summary>
            /// Это контрол для фильтрации в WebObjectListView.
            /// </summary>
            Filter
        }

        /// <summary>
        /// Причина создания контрола.
        /// </summary>
        public CreateControlReason ControlCreationReason { get; private set; }

        /// <summary>
        /// Тип свойства, для работы с которым создавался контрол.
        /// </summary>
        public Type PropertyType { get; private set; }

        /// <summary>
        /// Имя свойства, для работы с которым создаётся контрол.
        /// </summary>
        public string PropertyName { get; private set; }

        /// <summary>
        /// Тип, в котором находится свойство, для работы с которым создаётся контрол.
        /// </summary>
        public Type DataObjectType { get; private set; }
    }
}
```

## Пример
Пример работы делегата реализован на тестовом стенде:
"http://ru:6158/forms/DataEdit/TestChangeControlDelegate/TestChangeControlDelegateL.aspx"

Делегат можно определить следующим образом. При этом в контроле фильтрации, соответствующем свойству `DateTimePropertyWithDelegate` будет доступно задание даты и в фильтре будет отображаться надпись "По этому полю нельзя отфильтровать.".
```cs
/// <summary>
/// Обработчик события завершения инициализации.
/// </summary>
/// <param name="e">Параметры события.</param>
protected override void OnInitComplete(EventArgs e)
{
	base.OnInitComplete(e);
	WebObjectListView1.WebControlProvider.TuneControlDelegateMethod = ChangeControlDelegateMethod;
}

/// <summary>
/// Делегат, который поменяет настройки одного из контролов для отображения дат в строке фильтрации.
/// </summary>
/// <param name="control">Сам контрол.</param>
/// <param name="changeControlDelegateData">Параметры создания контрола (для чего был создан).</param>  
private void ChangeControlDelegateMethod(Control control, CreatedControlData changeControlDelegateData)  
{  
	if (control is DatePicker  
  	    && changeControlDelegateData.ControlCreationReason  
            == CreatedControlData.CreateControlReason.Filter  
            && changeControlDelegateData.DataObjectType == typeof(TestChangeControlDelegate)  
            && changeControlDelegateData.PropertyName  
            == Information.ExtractPropertyPath<TestChangeControlDelegate>(x => x.DateTimePropertyWithDelegate))  
        {  
        	var datePicker = (DatePicker)control;  
        	datePicker.OnlyDate = false;  
        	datePicker.DateFormat = "По этому полю нельзя отфильтровать.";  
        	datePicker.TimeFormat = string.Empty;  
        }  
}  
```  
 
  


