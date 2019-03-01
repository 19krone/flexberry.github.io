--- 
title: Reading belonging to different object classes in a single view 
sidebar: flexberry-orm_sidebar 
keywords: Flexberry ORM, class, object, idea 
summary: Features reading objects from different classes 
toc: true 
permalink: en/fo_reading-several-types-objects.html 
lang: en 
autotranslated: true 
hash: f20cf3a434a3b693d879b11477ee69ef95d01f8ab7588f5f397b51cce525c559 
--- 

To read many objects, you need (at least) to make settings [LoadingCustomizationStruct](fo_loading-customization-struct.html): 

* specify [data classes](fo_data-object.html), which reads ([LoadingTypes](fo_loading-customization-struct.html)); 
* specify common [view](fd_view-definition.html) ([View](fo_loading-customization-struct.html)). 

Thus, if there is a situation: 

![](/images/pages/products/flexberry-orm/additional-features/primer-8.jpg) 

and you must read all instances of the CDDD and the CDDA in the view "Main" for the Resource, then `LoadingCustomizationStruct` parameterized in the following way: 

```csharp
lcs = new LoadingCustomizationStruct(null);			
lcs.View=Information.GetView("The main thing", typeof(Ресурс));
lcs.LoadingTypes=new Type[]{typeof(CDDD), typeof(CDDA)};
``` 

Then you must call [LoadObjects(lcs)](fo_data-service.html). 

An example is available at [GitHub](https://github.com/Flexberry/FlexberryORM-DemoApp/blob/master/FlexberryORM/CDLIB/CDADMTEST/Form1.cs). 

To solve the opposite problem, namely, for editing objects-successors in a wider range of properties than the ancestors, could be used [adaptive view](fo_adaptive-views-details.html). 



 # Переведено сервисом «Яндекс.Переводчик» http://translate.yandex.ru/