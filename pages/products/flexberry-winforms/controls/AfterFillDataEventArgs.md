---
title: Получение информации об удачности загрузки ОbjectListView
sidebar: product--sidebar
keywords: Windows UI (Контролы)
toc: true
permalink: ru/after-fill-data-event-args.html
folder: product--folder
lang: ru
---

В обработчике события `ОbjectListView.AfterFillData` появилась возможность получить информацию об успешности загрузки. В качестве параметра события вместо типа `EventArgs` передается его наследник `AfterFillDataEventArgs`.
Тип `AfterFillDataEventArgs` имеет три свойства:
```cs
        /// <summary>
        /// Исключение, произошедшее во время загрузки
        /// </summary>
        public Exception Exception { get; private set;}
        /// <summary>
        /// Загрузка отменена пользователем
        /// </summary>
        public bool CanceledByUser { get; private set; }
        /// <summary>
        /// Загрузка успешно завершена
        /// </summary>
        public bool IsFillSuccessfullyCompleted { get; private set; }
```
Пример:
```cs
        private void objectListView1_AfterFillData(object sender, EventArgs e)
        {
            if (e is AfterFillDataEventArgs)
            {
                var afterFillDataEventArgs = e as AfterFillDataEventArgs;
                MessageBox.Show(
                    string.Format("CancelByUser: {0}, Exception: {1}, IsFillSuccessfullyCompleted: {2} ",
                    afterFillDataEventArgs.CanceledByUser, afterFillDataEventArgs.Exception, afterFillDataEventArgs.IsFillSuccessfullyCompleted));
            }
        }
```
Работы выполнены в рамках задания Flexberry '''2085'''.

 

