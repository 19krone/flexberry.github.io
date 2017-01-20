---
title: HighLighter
sidebar: product--sidebar
keywords: Windows UI (формы)
toc: true
permalink: ru/high-lighter.html
folder: product--folder
lang: ru
---

# HighLighter
'''HighLighter''' - класс, обеспечивающий подсветку активного контрола на форме.

### Объявление: 
Для его работы, в проекте должна быть ссылка на сборку `ICSSoft.STORMNET.Windows.Forms.AdditionalControls`

В [скобки программиста](programmer-brackets.html) `CustomMembers` поместить код:
```cs
// Объявление HighLighter'а HL
ICSSoft.STORMNET.Windows.Forms.HighLighter HL;
```
В конструкторе зависимой формы:
```cs  
// Создание объекта                            
HL = new ICSSoft.STORMNET.Windows.Forms.HighLighter(this);

// Задание цвета подсветки
HL.HighlightColor = System.Drawing.Color.FromArgb(150, 255, 150);
```

В конструкторе независимой формы:
```cs  
// Создание объекта                            
HL = new ICSSoft.STORMNET.Windows.Forms.HighLighter(form);

// Задание цвета подсветки
HL.HighlightColor = System.Drawing.Color.FromArgb(150, 255, 150);
```

Также можно настроить подсветку для нескольких форм сразу. Для этого необходимо следующее:
#В самом начале приложения подписаться на событие загрузки формы посредством [Desktop.GlobalWinformEvents.Load|Как-единообразно-обработать-все-формы-приложения].
#Определить список «changingFormTypes», куда записываются типы форм, для которых необходимо организовать подсветку.
#В обработчике включаем подсветку (важно: метод «HL.SubscribeHighliterManually();» доступен в версии Flexberry после 14.08.2014).

Настройка производится в приложении.

Пример

```

 [AccessType(ICSSoft.STORMNET.AccessType.none)]
 public class TestStandWinformsDesktop : ICSSoft.STORMNET.Windows.Forms.Desktop
    {
        
        ...
        
        // *** Start programmer edit section *** (TestStandWinformsDesktop CustomMembers)
        /// <summary>
        /// Список форм, для которых настроена подсветка и переход по Enter.
        /// </summary>
        private static List<Type> changingFormTypes = new List<Type>()
            {
                typeof(IIS.TestStandWinforms.WinformДомHighLighter),
                
            };

        /// <summary>
        /// Обработчик события загрузки формы.
        /// Используется для подписки необходимых форм на подсветку.
        /// </summary>
        /// <param name="sender">Инициатор события, форма.</param>
        /// <param name="e">Параметры события.</param>
        static void GlobalWinformEvents_Load(object sender, EventArgs e)
        {
            if (changingFormTypes.Contains(sender.GetType()))
            {
                Form currentForm = (Form)sender;
                ICSSoft.STORMNET.Windows.Forms.HighLighter HL;
                // Создание объекта                            
                HL = new ICSSoft.STORMNET.Windows.Forms.HighLighter(currentForm);
                HL.SubscribeHighliterManually();

                // Задание цвета подсветки
                HL.HighlightColor = System.Drawing.Color.FromArgb(150, 255, 150);
            }
        }

        // *** End programmer edit section *** (TestStandWinformsDesktop CustomMembers)

        ...

 [STAThread()]
 static void Main()
 {
    try
    {
         // *** Start programmer edit section *** (TestStandWinforms Before authorization)
         // Подписываемся на загрузку формы.
         Desktop.GlobalWinformEvents.Load -= GlobalWinformEvents_Load;
         Desktop.GlobalWinformEvents.Load += GlobalWinformEvents_Load;

         ...
         // *** End programmer edit section *** (TestStandWinforms Before authorization)
     ...
    }
 }
```

### Как работает:
Судя по всему, `HighLighter` подписывается на события `OnGotFocus` и `OnLostFocus` объектов формы и меняет их свойство `BackColor` на свой и обратно при срабатывании.

### Результат
Сравнение одной и той же формы с включенным Highlighter'ом и без:

{|
! Без Highlighter'a !! С Highlighter'ом
|-
| ![](/images/pages/img/page/HighLighter/HighlighterOff.gif)||![](/images/pages/img/page/HighLighter/HighlighterOn.gif)|}
|-
|}



