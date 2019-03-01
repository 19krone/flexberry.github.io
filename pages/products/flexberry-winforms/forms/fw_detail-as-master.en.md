--- 
title: Detail as a master 
sidebar: flexberry-winforms_sidebar 
keywords: Flexberry Winforms 
summary: Describes the procedure if necessary to make detail master of another object and be able to select objects from the list detaily forms listed possible problems 
toc: true 
permalink: en/fw_detail-as-master.html 
folder: products/flexberry-winforms/ 
lang: en 
autotranslated: true 
hash: 34f61a33d39ef84840dd4e9bf161ce848820543393e3b6d870fdfbfe4e4b10a9 
--- 

## Description 
![](/images/pages/products/flexberry-winforms/forms/connect-details-master.png) 

One feature of datalow is the lack of list form and edit form: both that and another is [GroupEdit](fw_group-edit.html) on the edit form of an aggregator. However, if the need arises to make detail master of another object, the first step is to create the edit form (and, consequently, [L-view](fd_l-view.html)). 

## Necessary actions 
* Create L-view for artisan of detail. 
* Create a [list](fd_key-concepts.html) for artisan of detail. 
* Configure the [E-submission](fd_e-view.html) artisan of detail. 
* Configure [LookUp's](fw_lookup.html). 

### to Create an L-representation 
To create an L-representation, it is necessary to go into the properties of the class of the workman lucapa (in our case - Stratiography), go to the tab "View" and create a new view, naming it `"СтрокаПогашенияПланаL"` 

![](/images/pages/products/flexberry-winforms/forms/connect-details-master-l-view.png) 

### to Create a list form 
To create the list, open the chart application and the forms created with the rapid prototyping. Create a new class, call it `СтрокаПогашенияПланаL`. Select the stereotype `listform`. Go to the class properties, in the tab "Composite view" select the view `СтрокаПланаПогашенияL` created in the previous step. 

![](/images/pages/products/flexberry-winforms/forms/connect-details-master-l-form.png) 

### to Configure E-submission 
To detail it was not possible to change the aggregating object must be removed from the E-presentation all references to it, and add links to the object for which he will be the master. 

![](/images/pages/products/flexberry-winforms/forms/connect-details-master-e-view.png) 

### Configure LookUp's 
The last step is to configure lyapov aggregating object of our "non-artisan of detail" (in our case, this object `Клиент`, which is an aggregator for `КредитнойКарты`). Go to the settings edit form class `КлиентE`, press the button `PropertyLookups` and choose the appropriate container (the form created in step 2). 

![](/images/pages/products/flexberry-winforms/forms/connect-details-master-lookups.png) 

## Error 
If something is made incorrectly, then when you try to open the object LookUp will appear error message "`No Such Container`". 


The same error occurs when trying to create a new object in the form of a list of detail as the edit form for him there. 



 # Переведено сервисом «Яндекс.Переводчик» http://translate.yandex.ru/