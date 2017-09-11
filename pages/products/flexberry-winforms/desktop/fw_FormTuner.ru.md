---
title: Настройка форм для приложения
sidebar: product--sidebar
keywords: Windows UI (формы), Конкретная реализация, ПНИПУ, Разработка
toc: true
permalink: ru/fw_form-tuner.html
folder: products/flexberry-winforms/
lang: ru
---

Достаточно часто возникает задача применить в run-time ко всем формам приложения какие-либо настройки. Особенно задача актуальна для независимых форм. В данном случае Вам поможет `UniversalFormTuner`, а точнее его наследник, определенный в прикладном приложении.


Последовательность действий такова:

#Добавить в прикладное приложение класс, наследующий от `ICSSoft.STORMNET.UI .UniversalFormTuner`.

#Переопределить метод 
```cs
public virtual void TuneForm( BaseWin form )
```
Параметр `form` – ссылка на экземпляр формы перед ее отображением.

#Присвоить свойству `UniversalFormTuner.StandardTuner` ссылку на экземпляр Вашего «тюнера».


Кроме того, для осуществления единообразной обработки форм приложения, можно подписаться на специальное глобальное событие (в методе `Main`):
```
static void Main()
...
// *** Start programmer edit section *** (Детейломания Main())
ICSSoft.STORMNET.Windows.Forms.WinApplication.SetUICultureAsRussian();
ICSSoft.STORMNET.Windows.Forms.Desktop.GlobalWinformEvents.Load += new EventHandler(GlobalWinformEvents_Load);
// *** End programmer edit section *** (Детейломания Main())
ICSSoft.STORMNET.Business.LockService.ClearAllUserLocks();
...
}
```

В обработчик этого события будет приходить форма в переменной sender. Собственно что с ней делать дальше - знаете сами. Например, можно все формы подписать на нажатие определённых клавиш:
```

// *** Start programmer edit section *** (ДетейломанияDesktop CustomMembers)
static void GlobalWinformEvents_Load(object sender, EventArgs e)
{
((Form)sender).KeyPreview = true;
((Form)sender).KeyPress += new KeyPressEventHandler(ДетейломанияDesktop_KeyPress);
}
static void ДетейломанияDesktop_KeyPress(object sender, KeyPressEventArgs e)
{
if (e.KeyChar == 13)
{
MessageBox.Show("Enter was pressed","Hello");
}
}
// *** End programmer edit section *** (ДетейломанияDesktop CustomMembers)
``` 

