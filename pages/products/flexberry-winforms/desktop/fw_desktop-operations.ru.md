---
title: Кнопка «Свернуть/развернуть папки» на рабочем столе
sidebar: flexberry-winforms_sidebar
keywords: Windows UI (формы)
summary: Объяснение как управлять видимостью кнопки __«Свернуть/развернуть папки»__ рабочего стола приложения, пример
toc: true
permalink: ru/fw_desktop-operations.html
folder: products/flexberry-winforms/
lang: ru
---

В панели инструментов рабочего стола имеется кнопка __«Свернуть/развернуть папки»__. Для ее отображения необходимо пристроить свойству `Operations` контрола рабочего стола значение `DesktopOperations.TreeExpandCollapse`. Проще всего сделать это в методе Main формы рабочего стола.

```csharp
static void Main()
{
    try
    {
		...

        КошкиИЛапыDesktop desktop = new КошкиИЛапыDesktop();
		
		...  

        desktop.desktopCtrl2.Operations = DesktopOperations.TreeExpandCollapse;
        Application.Run(desktop);
    }
    catch (System.Exception e)
    {
		...
    }
}
```