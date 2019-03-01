--- 
title: Creating and editing data classes 
sidebar: flexberry-designer_sidebar 
keywords: Flexberry Designer, the application structure, all forms of data classes 
summary: the Metadata, create and edit class and its views 
toc: true 
permalink: en/fd_create-data-class.html 
lang: en 
autotranslated: true 
hash: 05e053b24f732bb0d504d3350e9d32d0cddcfc6a200fa5c118e7418e7bfa63ab 
--- 

## Metadata class 

* `Заголовок` – a class name to display on формах; 
* `Атрибуты` – own attributes класса; 
* `Имя` – the name of the class in the project and in the source code of the application after генерации; 
* `Алиас` is the name that will be used for access to the class on bekende using the software interface, web сервиса; 
* `Хранимый` – set is a check mark indicates that the data objects need to be stored in the database данных; 
* `Хранилище` – the name of the corresponding table in the database for класса; 
* `Пакет` - used to specify the folder in the file system, which will generate files for this класса; 
* `Постфикс space имен` – additional "part" of a namespace, which will be added at the source code level приложения; 
* `Бизнес-сервер` – the corresponding business server associated with классом; 
* `Представления` – list of submissions класса; 
* `Типы хранилищ` – the list of databases for storage of data objects (used for when different classes need persistent data stored in different databases managed by different DBMS). 

## Creating and editing 

Create a data class is possible: 

* the link "Advanced -> Classes" in the main menu of the application 
* click "Add form edit" page of the application Structure 

Edit the data class is possible: 

* click "view the list of classes" on page Structure for your application 
* the link "Advanced -> Classes" in the main menu of the application, you can open a form with a list of all classes of the designed system with which you can proceed to edit the metadata of the class by clicking on the corresponding line of the list. 
* the allocation of class data in the left part of the page Structure of the application and the edit button. 

### Edit views 

Presentation for class edited on a separate form. In order to navigate in the view designer, you must create a new or select an existing submission to edit (click on the appropriate line). 

In the left part of the screen displays a tree with all the attributes of the corresponding data class, and the right tree with the attributes belonging to individual view. The attributes in the right tree, you can remove and add from the left tree. The tabs on the right side of the screen allow you to edit General properties of the representation and the particular attributes from the list selected. 



 # Переведено сервисом «Яндекс.Переводчик» http://translate.yandex.ru/