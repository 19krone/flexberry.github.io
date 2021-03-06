---
title: Подготовительный этап разработки веб-приложений
sidebar: guide-practical-guides_sidebar
keywords: guide
toc: true
permalink: ru/gpg_preparatory-stage.html
lang: ru
---

{% include important.html content="Описанный ниже алгоритм получения веб-приложения доступен после выполнения [Практического руководства по созданию UML-диаграмм](gpg_practical-guides-uml.html)." %}

## Постановка проблемы

Результатом выполнения предлагаемого практического примера будет `сгенерированный и откомпилированный код`, то есть готовое Веб-приложение.

Для того чтобы модуль генерации кода мог сгенерировать приложение, нужно создать:

* представления,
* классы форм для редактирования,
* классы форм для списков,
* класс приложения,
* а также выполнить определенные настройки.

Чтобы облегчить этот процесс, в [Flexberry Designer](fd_landing_page.html) используется [быстрое прототипирование](fd_using-quick-prototyping.html), которое выполняет эти действия определённым образом. В результате этого получается работающее приложение, которое может использоваться в качестве прототипа при работе с заказчиком на начальных стадиях проекта.

`Главное достоинство этого способа` - прототип получен почти «мгновенно», без ощутимых затрат времени. Впоследствии созданные при помощи прототипизации объекты можно модифицировать, приближая тем самым систему к требуемой функциональности.

## Предварительные требования для генерации веб-приложения

Для возможности создания [прототипа веб-приложения](fd_prototype-creation.html) должны быть выполнены следующие требования:

1.	Должен быть подключен модуль ASP.NET в приложении Flexberry Designer.
2.	В репозитории должна быть создана структура вплоть до системы. 
3.	Должна быть создана диаграмма классов.
4.	Должна быть установлена Visual Studio 2013 и выше.
5.	Должен быть установлен MS SQL Server 2008 и выше.

## Уточнение модели

Прототип приложения можно создать только при наличии [диаграммы классов](fd_class-diagram.html). В ней должны быть указаны все необходимые атрибуты и их типы, правильно описаны операции

Для уточнения модели необходимо:

1.	Открыть диаграмму классов `Сущности`, созданную в рамках [Практического руководства по созданию UML-диаграмм](gpg_practical-guides-uml.html).
2.	Указать типы атрибутов классов, как это сделано на следующей диаграмме:

![](/images/pages/guides/flexberry-aspnet/refined-ckass-diagram.png) 
 
__Примечание:__

* Типы атрибутов можно указать и при первом рассмотрении системы, но обычно на начальных этапах они опускаются в связи с неопределённостью или отсутствием необходимости в них. На этапе прототипирования типы должны быть указаны.
* Чтобы убедиться в корректности введённых атрибутов, можно посмотреть свойства данного класса (в контекстном меню класса выбрать пункт `Редактировать свойства`). 
* При генерации кода на диаграмме классов не должно быть связей типа агрегация (могут использоваться только ассоциация, композиция и наследование), а также связей с множественностью `один-к-одному` или `многие-ко-многим`.

3.Сохранить диаграмму.

## Перейти

* [Практическое руководство  «Делай как я»](gpg_landing-page.html) <i class="fa fa-arrow-up" aria-hidden="true"></i>
* [Настройка генератора скриптов для БД](gpg_configuring-script-generator-db.html) <i class="fa fa-arrow-right" aria-hidden="true"></i>
