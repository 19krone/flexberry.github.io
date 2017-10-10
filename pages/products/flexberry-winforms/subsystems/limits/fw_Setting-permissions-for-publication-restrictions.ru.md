---
title: Настройка прав доступа на публикацию ограничений
sidebar: flexberry-winforms_sidebar
keywords: Flexberry Security, Flexberry Winforms, Ограничения
toc: true
permalink: ru/fw_setting-permissions-for-publication-restrictions.html
folder: products/flexberry-winforms/
lang: ru
---

## Описание

Настраивается __AdvLimitComponent__ следующим образом:

* В свойстве __PublicateOperationId__ указвается id операции (по умолчанию "-1")

* В свойстве __PublicateAccess__ указывается возможность доступа по умолчанию (Если __PublicateOperationId__ <= 0 либо AzMan не может проверить доступ и вызывает ошибку)

## Настройка в Flexberry Security
Данная операция должна быть прописана с именем, соответствующим __PublicateOperationId__. Данное решение не является красивым, но применяется для обеспечения совместимости с системами, работающими на `AzMan` (для возможности быстрого перехода на [Flexberry Rights](rightservice-flexberry-rights.html)).


## Смотрите также

* [Как начать работу с подсистемой полномочий](how-to-start-work-with-right-manager.html).
* [Сценарии использования подсистемы полномочий](rights-scenarios.html).
* Все статьи категории "Полномочия".