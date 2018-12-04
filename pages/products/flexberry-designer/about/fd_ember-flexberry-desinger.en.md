---
title: Ember Flexberry Designer
keywords: Ember Flexberry Desinger, UML, основы проектирования, модули, настройка
summary: Общие сведения об Ember Flexberry Desinger
sidebar: flexberry-designer_sidebar
toc: false
permalink: en/fd_ember-flexberry-desinger.html
lang: en
---

**Ember Flexberry Designer** - CASE-инструмент с веб-интерфейсом [Flexberry Designer](fd_landing_page.html) предназначен для анализа и проектирования объектно-ориентированных систем, а также генерации прототипов веб-приложений на основе построенных моделей. Реализован с помощью фреймворка [Ember.js](https://ru.wikipedia.org/wiki/Ember.js).

Ember Flexberry Designer является [продуктом платформы Flexberry](fp_platform-structure.html).

`Ember Flexberry Desinger` может быть использован в двух режимах:

1. Создается отдельный сервис, позволяющий работать с различными проектами. В этом случае доступен список организаций (по аналогии с [Github](https://github.com)) и список проектов.
2. Работа с составной частью приложения. В таком случае Desinger загружается с выбранным проектом для конкретного решения.

## Основные понятия

`Метаданные приложения` – данные, описывающие структуру классов и их отношений, структуру связанных с ними форм и прочие артефакты, которые используются при проектировании и генерации прототипа приложения.

`Класс данных` - класс, соответствующий некоторой сущности предметной области. На диаграммах UML не имеет стереотипа, либо может иметь стереотип `implementation`. Экземплярами классов данных являются объекты данных. Однако термин «объект данных» периодически используется как синоним термина «класс данных».

`Собственный атрибут` – атрибут класса данных, который определен непосредственно в самом классе.

`Мастер` - класс данных со стороны множественности 1, либо 0..1 в UML-отношении «ассоциация» между классами данных.

`Детейл` – класс данных, связанный с агрегатором (являющийся «частью») в UML-отношении «композиция» между классами данных.

`Представление` – поименованный набор собственных или унаследованных атрибутов класса, а также атрибутов из других связанных классов (включая сами связи). Представления применяются при получении данных с бакенда и, соответственно, при чтении данных из базы дынных. Представления используются при чтении данных на формах приложения, а также для «явного» чтения данных внутри исходного кода приложения. На формах, в основном, используются два вида представления:

* _L-представление_ - используется на списковых формах;
* _E-представление_ - используется на формах редактирования и в компоненте для работы с детейлами.

`Списковая форма` – форма, которая обеспечивает пользовательский интерфейс для отображения списка объектов данных в некотором представлении, а также выполнения вспомогательных действий с этим списком (поиск, фильтрация, сортировка, настройка отображения, экспорт данных и пр.). С одним классом данных может быть связано несколько списковых форм. С точки зрения метаданных приложения, списковая форма – это класс со стереотипом `listform`.

`Форма редактирования` - форма, которая обеспечивает пользовательский интерфейс для создания или редактирования объекта данных в заданном представлении. С одним классом данных может быть связано несколько форм редактирования. С точки зрения метаданных приложения форма редактирования – это класс со стереотипом `editform`.
Класс приложения – специальный класс в метаданных приложения, в котором хранятся общие для всего проектируемого приложения настройки – например, структура навигации (меню), конфигурация приложения и т.п. Данный класс имеет стереотип `application` в метаданных приложения.

`Бизнес-сервер` – класс, в который выносятся методы, срабатывающие «автоматически» после вставки, изменения и удаления данных в объекте данных определенного типа перед отправкой соответствующих изменений в базу данных (аналог триггеров в базах данных, но на уровне исходного кода приложения), а также сопутствующая бизнес-логика, связанная с соответствующим классом данных. С точки зрения метаданных приложения бизнес-сервер – это класс со стереотипом `businessserver`.

`Сервис генерации` – дополнительное программное обеспечение на стороне сервера, обеспечивающее возможность генерации прототипа приложения на основе метаданных проектируемого приложения.

## Режимы работы Flexberry Designer

### С «жестко» заданным проектом

В этом случае ID проекта указывается в конфигурации перед сборкой приложения. В таком режиме при запуске приложения сразу откроется форма с структурой указанного в конфигурации проекта.
 
ID проекта при этом указывается в файле `environment.js` приложения:

```javascript
var ENV = {    
    …
    APP: {
      …
      fdCurrentProjectContext: {
        singleModeStageId: '...',
      },
      …
    },
    …
};
```

### Без «жесткой» привязки к проекту

В этом случае доступна работа с множеством проектов, сгруппированных по организациям. 
При режиме работы без жесткой привязки к проекту, перед началом работы над проектом требуется сначала выбрать организацию, затем необходимо создать или выбрать проект и после выбора проекта откроется форма для редактирования структуры приложения.

### Организации

Список организаций, для которых планируется создание сервиса. Внутри организации расположен список проектов (решений).

### Проекты

Проект - это собственно решение, прикладная система. Каждый проект имеет собственную структуру метаданных (классы и формы).

### Структура приложения

Структура приложения - это основная форма, которая является ключевой для создания приложения. Она состоит из:

* _левого дерева_ (список классов). Это перечнь всех классов данных проектируемого приложения, а также все списковые формы и формы редактирования, привязанные к соответствующим классам данных (вложенные узлы). Классы разных типов имеют разную иконку. Левое дерево позволяет создавать/удалять/редактировать классы данных и формы, получить список классов в виде таблицы (аналогично менеджеру классов в декстопном варианте дизайнера).
* _правого дерева_ (структура конечного приложения) для редактирования навигационной структуры (структуры меню) проектируемого приложения. В данном дереве можно создавать меню произвольной вложенности, группируя элементы меню по «папкам» на различных уровнях. Элементами навигации (не считая «папки», которые используются для группировки элементов) могут быть списковые формы, формы редактирования или пункты меню, ссылающиеся на произвольный адрес URL. Для него доступны операции:

    * добавление нового элемента навигации (пункта меню) со ссылкой на произвольный адрес URL;
    * редактирование свойств (заголовка и описания) выбранного элемента навигации;
    * удаление элемента навигации;
    * добавление новой «папки» в структуру навигации;
    * изменение порядка элементов навигации (перемещение вверх и вниз);
    * сохранение структуры навигации.

Для добавления списковой формы или формы редактирования (из списка всех возможных форм, которые отображаются в левом дереве), необходимо выбрать соответствующую форму в левом дереве, затем выбрать соответствующую «папку» в правом дереве и нажать на кнопку добавления формы в навигационную структуру.
* вкладок, позволяющих настраивать и редактировать свойства класса `application`, стадии и формы.