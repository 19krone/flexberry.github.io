---
title: Фокус ввода и «Ctrl+S»
sidebar: flexberry-winforms_sidebar
keywords: Windows UI (формы)
toc: true
permalink: en/fw_focus-and-ctrl-s.html
folder: products/flexberry-winforms/
lang: en
---

При сохранении формы редактирования по комбинации __«Ctrl+S»__ фокус остается на активном контроле, текущее значение попадает в объект данных с помощью вызова `EditManager.ApplyDataFromControl(ActiveControl)`.<br>
