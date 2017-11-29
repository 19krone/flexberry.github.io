---
title: MongoDB
keywords: NoSQL, BigData
sidebar: guide-base-tech_sidebar
toc: true
permalink: ru/gbt_mongodb.html
lang: ru
---


## Краткое описание

MongoDB — написанная на языке C++ документоориентированная NoSQL система управления базами данных с открытым исходным кодом, не требующая описания схемы таблиц (schemaless).

MongoDB имеет следующие уровни представления данных:
1. Документ - JSON-объект имеющий произвольное число полей. Поля могуть хранить как простве значение, так к воженные объекты и массивы.
2. Коллекция (таблица)- однотипные документы хранятся в отдельной коллекции. Документы в коллекции могуть быть проиндекирован. Доступ к докумениту возможен как по ключу, так и по значению полей.
3. База данных - набор коллекций.

Поддержка MongoDB реализована для большинства языков программирования:
- C;
- C++;
- C#;
- Java;
- Node.js;
- Perl;
- PHP;
- Python;
- Ruby;
- Scala.

Отличия MongoDB от реляционных баз данных:
- Не  поддерживаются транзации. Атомарность гарантируется только на уровне целого документа, то есть частичного обновления документа произойти не может.
 - Отсутствие механизма «изоляции». Любые данные, которые считываются одним клиентом, могут параллельно изменяться другим клиентом.
 
 Преимущества MongoDB перед реляционными базами:
 - Поддержка горизонтального масштабирования с репликацией данных. Данные могут храниться на произвольном числе серверов. Репликация обеспечивает отказоустойчивость системы с поддержкой функционала при выходе узлов из строя.
 - Формат хранения данных (документ) близок к формату представления данных в языках программирования (объектов) не требуется сложных и дорогостоящих запросов для получения нужного объекта.
- Поддержка операций MapReduce для массовой параллельной обработки данных.


##  Ссылки на материалы для изучения

* [Getting Started with MongoDB (MongoDB Shell Edition)](https://docs.mongodb.com/getting-started/shell/);
* [MongoDB Краткое руководство](http://www.w3ii.com/ru/mongodb/mongodb_quick_guide.html);
* [Руководство по MongoDB (Записки задумчивого программиста)](http://proselyte.net/tutorials/mongodb/);
* [Руководство по безопасности MongoDB](http://security-corp.org/administration/sys_admin/39539-rukovodstvo-po-bezopasnosti-mongodb.html)

### Презентация
* [MongoDB вводная лекция](https://www.youtube.com/watch?v=tgckAOyjXPI)

### Рекомендованные книги

* [MongoDB в действии](https://www.ozon.ru/context/detail/id/8688130/);
* [MongoDB в действии (электронный вариант)](https://cafe-aristokrat.nethouse.ru/static/doc/0000/0000/0165/165988.c2f3acpbax.pdf)
* [The Little MongoDB Book](http://www.pvsm.ru/download/mongodb-ru.pdf);


## Программное обеспечение

* [Install MongoDB](https://docs.mongodb.com/manual/installation/);
* [Официальный Docker-образ MongoDB](https://hub.docker.com/_/mongo/)
* [Официальный Docker-образ WEB-интерфейса MongoDB](https://hub.docker.com/_/mongo-express/)

## Лабораторные работы и практические задания

Для установки mongoDB удобнее всего воспользоваться [docker-образом MongoDB](https://hub.docker.com/_/mongo/).

Запуск сервера производится командой:
```sh
docker run --name mongodb -p 27017:27017 -d mongo
```
Для работы с сервером mongo в конейнере рекомендуется запустить в рамках запущенного контейнера mongo-shell командой:
```sh
docker exec -it mongodb mongo
```

В качестве практических заданий  для лабораторных работ можно использовать [Задания к лабораторной работе 5 MongoDB](https://github.com/mesdt/course/wiki/Tasks-Mongo). На данной странице приведены как [ссылка на тестовые наборы данных](https://yadi.sk/d/3l92O1G6fJst5), так и список заданий по выполнению операций на данных наборах данных.

## Примеры

Примеры выполнения CRUD и aggregation операций над указанными в предыдущем разделе наборами данных приведены на страницах: 
* [Команды CRUD в MongoDB](https://github.com/mesdt/course/wiki/Cheat-list-Mongo)
* [Aggregation Framework в MongoDB](https://github.com/mesdt/course/wiki/Cheat-list-Mongo-Aggregation-Framework)

## Возможности по сертификации

* [MongoDB Professional Certification Program ](https://university.mongodb.com/certification)
* [Сертификация mongoDB](https://habrahabr.ru/post/273011/)

## Перейти

* [Разработка мобильных приложений](gbt_mobile.html)
* [Главная страница курса](gbt_landing-page.html)
