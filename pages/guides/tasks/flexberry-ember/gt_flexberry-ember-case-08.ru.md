---
title: Вариант 8 - «Прогноз погоды»
keywords: Tasks
sidebar: guide-tasks_sidebar
toc: true
permalink: ru/gt_flexberry-ember-case-08.html
lang: ru
summary: Вариант сквозного задания на проектирование и разработку с использованием фреймворка Flexberry Ember
---

## Задание

В рамках выполнения практической части курса вами будет разработан сквозной пример: приложение «Прогноз погоды» (ИС для ведения прогноза погоды для различных территорий).

Первая часть практического задания будет посвящена освоению базовых технологий, таких как C#, базы данных, клиентские технологии и т.п., вторая часть будет включать изучение возможностей платформы Flexberry для эффективного создания приложений.

## Общее описание предметной области

Каждые 2 часа специалист метеорологической службы запускает алгоритм расчёта прогноза погоды для указанной территории. Алгоритм может выдавать экстремальные значения, которые корректируются в ручном режиме (например, -150 градусов в июне). Пользователи прогноза погоды получают доступ через интернет и могут выбирать территорию, для которой строится прогноз. Прогноз доступен на месяц вперёд от текущей даты. Также пользователь может подписаться на уведомление по E-Mail о предстоящем природном катаклизме с указанием интервала времени до его начала и территории.  

Технические требования:

*	Приложение реализуется в виде [SPA-приложения](https://ru.wikipedia.org/wiki/%D0%9E%D0%B4%D0%BD%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%87%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5) с бакендом на C# и фронтендом на EmberJS.
*	Данные хранятся в БД Postgres.

## Практическое задание №1 - Серверная разработка (C#, .NET, ASP.NET)

Для реализации потребуется:

* Microsoft Visual Studio 2017
* Git for Windows

### Задание

Требуется реализовать алгоритм имитирующий работу системы прогноза погоды. На вход нужно подать id территории, на выходе должен быть перечень параметров прогноза по каждому из дней на 30 дней относительно текущей даты. Параметры прогноза погоды:
* Дата
* Температура воздуха в градусах цельсия
* Облачность
* Явления погоды
* Давление в мм ртутного столба
* Направление ветра
* Скорость ветра
* Скорость ветра в порывах

Прогноз должен быть равномерным, то есть изменения погоды в различных параметрах должны быть относительно плавными без резких скачков в разные стороны. Параметры должны быть согласованы между собой, т.е. +28 градусов и снег вместе не встречаются. Добавить 5% отклонений алгоритма, которые будут давать резко произвольные, но непротиворечивые показания отдельных параметров, которые потребуется корректировать синоптикам в ручном режиме.  
Реализацию следует сделать в виде .net-библиотеки и подготовить модульные тесты для неё (xUnit), продемонстрировать процент покрытия кода модульными тестами (чем больше, тем лучше).

### Предоставление результатов выполнения работы на проверку

Реализованное решение (Visual Studio Solution) полностью разместить в репозитории на GitHub (решение должно компилироваться и запускаться). Ссылку на репозиторий предоставить преподавателям курса.

## Практическое задание №2 - Клиентская разработка (HTML, CSS, JS, jQuery)

Для реализации потребуется:

* Редактор кода для клиентской разработки: Visual Studio Code
* Git for Windows

### Задание

С использованием возможностей HTML, CSS, JS, jQuery сверстать форму, на которой пользователь может удобным образом просмотреть прогноз погоды на несколько возможных интервалов: 7 дней, 14 дней, 30 дней. Интервалы должны переключаться вкладками. 7 дней оформляются в виде одной строки. 14 дней - две строки по 7 дней в строке, 30 дней - 3 строки по 10 дней. Каждая ячейка с датой должна включать в себя всю информацию о погоде в краткой форме. По клику на ячейку должна открываться всплывающая форма с подробной информацией, когда каждый параметр погоды подписан.  

### Предоставление результатов

Реализованный проект разместить в репозитории на GitHub в виде встроенных страниц GitHub Pages, позволяющих просматривать готовый результат. Ссылку на репозиторий и опубликованный таким образом проект предоставить преподавателям курса.

## Практическое задание №3 - Клиентская разработка с использованием SPA-фреймфорка (EmberJS)

Для реализации потребуется:

* Редактор кода для клиентской разработки: Visual Studio Code
* Git for Windows

### Задание

Требуется реализовать EmberJS приложение, в котором будет реализована форма, на которой пользователь может удобным образом просмотреть прогноз погоды на несколько возможных интервалов: 7 дней, 14 дней, 30 дней. Интервалы должны переключаться вкладками. 7 дней оформляются в виде одной строки. 14 дней - две строки по 7 дней в строке, 30 дней - 3 строки по 10 дней. Каждая ячейка с датой должна включать в себя всю информацию о погоде в краткой форме. По клику на ячейку должна открываться всплывающая форма с подробной информацией, когда каждый параметр погоды подписан. Предусмотреть режим редактирования, который доступен пользователю метеорологической службы. В режиме редактирования можно изменять значения параметров погоды.  

В виде EmberJS-утилиты требуется реализовать алгоритм имитирующий работу системы прогноза погоды (см. задание №1).

Отображение прогноза погоды требуется реализовать в виде компонента, в который передаётся EmberJS-модель. EmberJS-модель, следует получать из EmberJS-утилиты в хуке model роута формы, на которую будет добавлен компонент.  

### Предоставление результатов

Реализованный проект разместить в репозитории на GitHub в виде проекта EmberJS и опубликованного приложения в GitHub Pages, которые позволяют просматривать готовый результат. Ссылку на репозиторий и опубликованный таким образом проект предоставить преподавателям курса.

## Практическое задание №4 - Базы данных

Для реализации потребуется:

*	Postgres
*	pgAdmin
*	Git for Windows

### Задание

Для указанной предметной области реализовать базу данных, заполнить базу скриптами (минимум по 5 записей на таблицу). Реализовать скрипты по созданию ограничений, индексов. 

Подготовить SQL-скрипты для получения следующей информации:

1. Вывести топ-5 территорий, в которых меньше всего дождливых дней
2. Вывести информацию о средней температуре на указанную дату по всем территориям
3. Вывести информацию о пользователе, который чаще остальных корректирует данные
4. Вывести информацию о температурных рекордах для указанной территории за всё время наблюдения
5. Вывести список территорий, на которых не было осадков в течение 30 дней подряд и наоборот, осадки не прекращались в течение 30 дней подряд

### Предоставление результатов

Реализованные скрипты создания БД и заполнения, бекап БД закоммитить в GitHub-репозиторий. Ссылку на репозиторий предоставить преподавателям курса.

## Практическое задание №5 - Проектирование ИС

Для реализации потребуется:

*	Flexberry Designer

### Задание

Нарисовать UML-диаграммы для обозначенной предметной области. Состав диаграмм определяется самим слушателем курсов, но должен обеспечивать полноценное описание предметной области.

### Предоставление результатов

Результатом работы является выгруженная в формате CRP стадия из Flexberry Designer. Стадию (файл с расширением *.CRP) следует закоммитить в репозиторий на GitHub, ссылку предоставить преподавателям курса.

## Практическое задание №6 - Объектный дизайн и генерация приложений

Для реализации потребуется:

*	Flexberry Designer
*	Microsoft Visual Studio 2017
*	Postgres
*	Git for Windows

### Задание

Выполнить объектный дизайн и генерацию Ember-приложения для описанной предметной области. В качестве основы использовать реализованные ранее UML-модели. Генерация приложения и БД должна быть выполнена средствами Flexberry Designer приложение должно соответствовать требованиям и быть полностью работоспособным. Представления должны быть качественно настроены, подписи к классам и атрибутам на формах должны быть адекватными. Перечень форм и атрибутивный состав должны соответствовать предметной области и покрывать все требуемые бизнес-функции.

### Предоставление результатов

Сгенерированное приложение и скрипты создания БД следует выложить в репозиторий на GitHub. Предоставить преподавателям ссылку на репозиторий.

## Практическое задание №7 - Разработка бизнес-логики приложений

Для реализации потребуется:

* Flexberry Designer
* Microsoft Visual Studio 2017
* Postgres
* Git for Windows

### Задание

В сгенерированном при помощи Flexberry Designer приложении требуется реализовать следующую бизнес-логику.

1. Реализовать бизнес-сервер, который будет контролировать, что в прогнозе погоды нет противоречивых параметров (например, снег в +25 и т.п.).
2. Реализовать бизнес-сервер, который будет вместо удаления объектов системы переводить их в состояние архивного объекта (для более точной настройки алгоритма прогнозирования).
3. Реализовать бизнес-сервер, который будет контролировать, что в список отслеживания катоклизмов добавляется территория, которой там ещё нет, аналогично для удаления территория должна в нём быть.
4. Добавить не хранимое поле в класс Сотрудник, которое будет представлять ФИО одной строкой из Фамилии Имени и Отчества.
5. Добавить строковое не хранимое поле, в котором будет собрана вся необходимая информация о прогнозе на конкретный день.

### Предоставление результатов

Доработанная бизнес-логика должна быть включена в разрабатываемое приложение и закоммичена в соответствующий репозиторий. Ссылка на репозиторий предоставляется для проверки преподавателям курса.

## Практическое задание №8 - Разработка UI-логики приложения

Для реализации потребуется:

*	Microsoft Visual Studio 2017
*	Postgres
*	Редактор кода для клиентской разработки: Visual Studio Code
*	Git for Windows

### Задание

Привязать реализованные ранее EmberJS дополнительные формы и компоненты к данным из БД.  
Перенести в сгенерированное приложение и реализовать интеграцию формы из задания №3 с бизнес-логикой приложения. 
На форме для элементов управления с выбором - данные должны браться из БД (через ORM и Lookup). Заполнение данных также должно работать с сохранением в БД. 
Требуется настроить красивый внешний вид для всех форм приложения. Улучшить визуальную тему оформления. Реализовать ярлыки на рабочем столе приложения для быстрого доступа к часто используемым функциям.  
Реализовать дополнительные формы, которые будут выводить результаты выполнения запросов из задания по БД.

### Предоставление результатов

Доработанная UI-логика должна быть включена в разрабатываемое приложение и закоммичена в соответствующий репозиторий. Ссылка на репозиторий предоставляется для проверки преподавателям курса.

## Практическое задание №9 - Функциональные подсистемы Flexberry

Для реализации потребуется:

*	Flexberry Designer
*	Microsoft Visual Studio 2017
*	Редактор кода для клиентской разработки: Visual Studio Code
*	Postgres
*	Git for Windows

### Задание

Для реализованного приложения настроить подсистему полномочий. Сотрудники метеорологической службы должны заводиться администратором приложения, остальные пользователи регистрируются самостоятельно (упрощённая схема). Авторизация на основе форм. Создать иерархию ролей, добавить операции на просмотр сведений о внутреннем устройстве прогноза. Настроить несколько ролей и назначить эти роли пользователям.  
Настроить подсистему аудита. В разрабатываемом приложении все изменения объектов данных должно фиксироваться в подсистеме аудита. В навигационное меню следует добавить формы аудита, которые должны показываться только администраторам.

### Предоставление результатов

Доработанное приложение должно быть закоммичено в соответствующий репозиторий. Дополнительно в репозиторий должны быть добавлены SQL-скрипты, которые нужно выполнить для функционирования приложения с подсистемой полномочий и аудита. Ссылка на репозиторий предоставляется для проверки преподавателям курса.
