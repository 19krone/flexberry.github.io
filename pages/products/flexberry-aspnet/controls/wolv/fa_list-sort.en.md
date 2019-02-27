--- 
title: Sorting for WebObjectListView 
sidebar: flexberry-aspnet_sidebar 
keywords: Flexberry ASP-NET 
toc: true 
permalink: en/fa_list-sort.html 
lang: en 
autotranslated: true 
hash: 3a02d5cedf073bd77d1d2b233f48d738dd82ad562a93bdeee7ef0b40e9957799 
--- 

Lists allow you to sort the contained objects in specific columns. The user can set the necessary sorting. Also sorting the list can be customized from the code. 

## Sorting lists WOLV 

Sort columns [WebObjectListView](fa_web-object-list-view.html) by specifying properties `.InitialColumnsSort` type `ICSSoft.STORMNET.Business.ColumnsSortDef[]`. 

Example: 

```csharp
wolv.InitialColumnsSort = new ColumnsSortDef[] 
{
    new ColumnsSortDef("Name", SortOrder.Asc),
    new ColumnsSortDef("Registration", SortOrder.Asc),
};
``` 

Here `ColumnsSortDef` the constructor takes 2 parameters: the name of the column `string` and method of sorting type `ICSSoft.STORMNET.Business.SortOrder` (Asc, Desc, None). 

The sort priority determines the order of elements in the array `ColumnsSortDef`. 

### Access to current sorting settings in the heirs 

Current settings [WebObjectListView](fa_web-object-list-view.html) consist of imposed by the developer through a public instance property `InitialColumnsSort` settings made by the user via the interface [WebObjectListView](fa_web-object-list-view.html). 

To access the aggregated current sorting settings through a protected virtual property `ActualColumnSort` in descendant classes. 




 # Переведено сервисом «Яндекс.Переводчик» http://translate.yandex.ru/