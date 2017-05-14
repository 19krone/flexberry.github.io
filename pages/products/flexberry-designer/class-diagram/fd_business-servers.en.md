---
title: Бизнес-серверы (классы со стереотипом businessserver) 
sidebar: flexberry-designer_sidebar
keywords: Flexberry Designer, Public, Businessserver
toc: true
permalink: en/fd_business-servers.html
folder: products/flexberry-designer/class-diagram/
lang: en
---

Для описания [бизнес-сервера](fo_business-servers-wrapper-business-facade.html) необходимо создать на диаграмме класс со [стереотипом](fd_key-concepts.html) `businessserver`.

Например:

![](/images/pages/products/flexberry-designer/class-diagram/businessserver.png)

## Что генерируется

* Код [бизнес-сервера](fo_business-servers-wrapper-business-facade.html): [класс, наследующийся от ICSSoft.STORMNET.Business.BusinessServer](fo_testing-user-operations-dataservice.html), методы генерируются как виртуальные методы с соответствующими параметрами и модификаторами. Тело метода пустое со [скобкой программиста](fo_programmer-brackets.html) для внесения кода метода. UML-атрибуты не генерируются, т.к. объекты [бизнес-сервера](fo_business-servers-wrapper-business-facade.html) не имеют состояния, о чём генератором выдаётся соответствующее предупреждение. 
* Указанные в свойствах заглушки для [бизнес-сервера](fo_business-servers-wrapper-business-facade.html). 
* [Бизнес-фасад](fo_business-servers-wrapper-business-facade.html).

# Свойства бизнес-сервера

![](/images/pages/products/flexberry-designer/class-diagram/bsprops1.jpg)

Свойство | Описание | Генерация в .Net-язык
:----------------------|:----------------------------|:--------------------------------------------
`Name` | имя UML-класса | Имя .Net-класса бизнес-сервера
`Description` | некоторое описание класса | `DocComment` перед определением класса
`Packet, NamespacePostfix` | позволяют настроить сборку и пространство имен, в которое должен генерироваться тип | см. [Расположение сборок после генерации кода](fo_location-assembly-after-code-generation.html).
`PBMembers` | позволяет указать, необходима ли скобка программиста внутри класса для "ручного" внесения членов класса | Если галочка указана - генерируется [скобка программиста](fo_programmer-brackets.html) для "ручного" внесения членов класса.
`GenerateComPlusServer` | | Если галочка установлена, - генерируется класс-заглушка (обёртка) в отдельной сборке, для обращения к бизнес-серверу через COM+.
`ComPlusServerOptions` | | Указывает для COM+ - заглушки управление транзакционностью COM+ по-умолчанию, в терминах COM+. Влияет на генерацию атрибута ``` [Transaction(TransactionOption.XXXXXXX)] ``` непосредственно перед классом заглушки
`GenerateHTTPRemoteServer` | | Если галочка установлена, - генерируется класс-заглушка (обёртка) в отдельной сборке, для обращения к бизнес-серверу через Remoting, организованный через протокол HTTP.

{% include note.html content="Свойства атрибутов бизнес-сервера не учитываются, так как не учитываются сами атрибуты. Свойства и генерация методов для бизнес-сервера происходит, как описано [в статье  Методы классов и параметры методов](fd_methods-parameters.html)." %}
