---
title: Изменение внешнего вида контрола LookUp
sidebar: flexberry-winforms_sidebar
keywords: Windows UI (Контролы)
summary: Described ways to change the appearance of buttons LookUp controls, images, size, borders
toc: true
permalink: en/fw_lookup-appearance.html
lang: en
---

## Настройка изображений
Существует два способа изменить изображения на кнопках LookUp’а.

1. В случае если требуется изменить изображения в рамках всего приложения, необходимо инициализировать статический ImageList при запуске приложения. В этом списке должны присутствовать изображения с именами "LookUp", "Clear" и "Edit".
<br>Пример:<br>
```csharp
LookUp.UserImageList.Images.Add("LookUp", Properties.Resources.LookUpImage);
LookUp.UserImageList.Images.Add("Clear", Properties.Resources.ClearImage);
LookUp.UserImageList.Images.Add("Edit", Properties.Resources.EditImage);
```
2. Для конкретного экземпляра LookUp’а с помощью свойства `UserImageList` можно назначить пользовательский ImageList, в котором также должны быть изображения с именами "LookUp", "Clear" и "Edit".


## Размер кнопок
Размер кнопок задается с помощью свойства `ButtonSize`, при изменении данного свойства должно выполнится перевычисление размера всего контрола.

## Границы кнопок

За отображение границ кнопок отвечает свойство `ButtonBorder`.