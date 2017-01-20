---
title: Как включить лог ошибок
sidebar: product--sidebar
keywords: Flexberry Winforms, Windows UI (формы), Развёртывание
toc: true
permalink: ru/fw_include-error-log.html
folder: products/flexberry-winforms/
lang: ru
---

Чтобы включить лог ошибок достаточно указать такой атрибут в файле конфигурации:
```xml   
<add key="ErrorLog" value="true" />
```
Все ErrorBox-ы будут записывать ошибки в csv-файл в папку с приложением.
