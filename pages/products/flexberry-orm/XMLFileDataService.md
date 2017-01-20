---
title: XMLFileDataService
sidebar: product--sidebar
keywords: Flexberry ORM, Public
toc: true
permalink: ru/x-m-l-file-data-service.html
folder: product--folder
lang: ru
---

# XMLFileDataService
'''XMLFileDataService''' - сервис данных предназначенный для работы с базой данных в формате XML. Для корректной работы сервиса данных необходима XSD-схема базы данных и XML-файл базы данных. Получить их можно воспользовавшись [XMLSchemaGenerator](x-m-l-schema-generator.html) (подключаемый к Flexberry плагин для генерации XSD-схемы базы данных).

Для работы с данными в формате XML используется '''System.Data.DataSet''' поддерживающий транзакции и SQL-запросы. Также DataSet поддерживает ограничения ссылочной целостности. Для работы '''XMLFileDataService''' необходимо включать ограничения ссылочной целостности. Включение ограничений ссылочной целостности осуществляется посредством включения свойства '''EnforceConstraints'''. [XMLSchemaGenerator](x-m-l-schema-generator.html) по умолчанию это свойство проставляет в true.

В качестве '''CustomizationString''' указывается путь до XSD и  XML файлов без указания расширения (оба файла должны иметь одинаковое имя).

К примеру, в папке C:\DataBase\ лежат файлы base.xsd и base.xml, тогда путь будет выглядеть следующим образом: '''C:\DataBase\base'''
 

