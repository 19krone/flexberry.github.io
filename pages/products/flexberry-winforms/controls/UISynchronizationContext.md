---
title: Запуск кода в основном потоке приложения из другого потока
sidebar: product--sidebar
keywords: Windows UI (Контролы), Windows UI (формы)
toc: true
permalink: ru/u-i-synchronization-context.html
folder: product--folder
lang: ru
---

Одно из основных правил многопоточной разработки для форм Windows гласит: ''«Обращение к элементу управления должно производится из того потока, в котором этот элемент управления был создан»''. Обычно эта задача решается вызовом методов `Control.Invoke` (синхронный запуск делегата) и `Control.BeginInvoke` (асинхронный запуск делегата).
Однако иногда возникает необходимость запустить код в основном потоке приложения при отсутствии ссылки на контрол, созданный в этом потоке. Для решения задачи запуска кода в основном потоке из другого потока в WinForms применяется класс `SynchronizationContext`. В Flexberry Platform обратиться к контексту синхронизации можно посредством вызова `UISynchronization.Context`, статическое поле `Context` инициализируется в конструкторе формы рабочего стола.

'''Пример:'''

```cs
if (UISynchronization.Context!=null)
UISynchronization.Context.Send((delegate
       {
       	bugReportProvider.SaveError(_screenShots, sysInfo, exceptions[0] as Exception);
       }), null);
```


