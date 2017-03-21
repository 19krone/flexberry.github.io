---
title: FileControl (Web)
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET, JavaScript API, Web UI (Контролы)
toc: true
permalink: ru/fa_file-control-web.html
folder: products/flexberry-aspnet/
lang: ru

---

* **Платформа:** [FlexberryASP.NET](fa_flexberry-a-s-p-n-e-t.html)
* **Компонент:** [Web-контролы и web-компоненты](fa_web-controls.html)
* **Предназначение:** Web-контрол для работы с типом данных ICSSoft.STORMNET.FileType.File в web-приложении.
* **JavaScript API:** да

## Описание
Это контрол для работы с типом данных `ICSSoft.STORMNET.FileType.File` в веб-приложении. Файлы сохраняются в БД в виде сериализованной 
строки, поэтому данный контрол предназначен для работы с небольшими файлами.

В браузере пользователь имеет возможность выбрать файл из своей файловой системы и сохранить его в БД в соответствующем поле объекта данных, на которое установлен биндинг.

Выглядит контрол следующим образом:
![](/images/pages/products/flexberry-aspnet/aspnet/file-control.png)

Вначале указывается наименование текущего сохраненного или выбранного файла.Далее идут кнопки: 

* Выбрать файл - открыть диалог для выбора файла,
* Скачать файл - скачать текущий сохраненный файл из БД,
* Сбросить файл - сбросить сохраненный или только что выбранный файл.

Кнопка "Скачать файл" будет недоступна, если файл отсутствует в БД (т.е. соответствующее поле объекта данных равно null).
Примечание: если вы выберете новый файл, или нажмете кнопку "Сбросить файл", то кнопка "Скачать файл" будет скачивать старый файл, тот, что в БД, до тех пор, пока вы не сохраните объект данных (форму редактирования). 

Внимание: нажатие на любую из трех кнопок не производит никаких изменений в БД, изменения произойдут только при сохранении формы редактирования.

Кнопка "Сбросить файл" сбрасывает текущий выбор, после чего в компоненте отобразится надпись "(нет файла)". При сохранении формы редактирования старый файл в БД будет удален, на его место запишется значение null.

Компонент поддерживается в [AjaxGroupEdit](fa_ajax-group-edit.html).

## Ограничение на размер загружаемого файла
По умолчанию ограничение берется из опции [maxRequestLength](https://msdn.microsoft.com/en-us/library/e1f13641(v=vs.100).aspx) в файле конфигурации приложения (web.config). Значение данного атрибута по умолчанию - 4 МБ, если он отсутствует в файле конфигурации.
Данное ограничение может быть переопределено в свойстве FileControl.MaxValueSize. Новое значение не может быть меньше 1 и больше maxRequestLength, в противном случае возникнет исключение.

Если пользователь выберет файл, размер которого превышает заданное ограничение, то он получит сообщение о превышении допустимого размера файла, после чего выбранный файл будет сброшен: 

![](/images/pages/products/flexberry-aspnet/aspnet/file-control-max-file-size.png).

Примечание: ограничение на размер запроса может быть установлено средствами IIS, которое может расходиться с атрибутом maxRequestLength. Такая ситуация не контролируется компонентом FileControl.


## Подключение FileControl (Web) к приложению
Для того, чтобы FileControl появился на форме редактирования, нужно его добавить в `aspx`-разметку. 

```html
<ac:FileControl ID="ctrlFile" runat="server"/>
```

Контрол располагается в сборке `ICSSoft.STORMNET.Web.AjaxControls.dll`.

Для добавления в контролы, которые формируются динамически (например, [AjaxGroupEdit](fa_ajax-group-edit.html)), нужно прописать в [WebControlProvider](fa_web-control-provider.html) следующие строки:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="WebControlProvider.xsd">
<!-- ... -->
  <propertytype name="File">
    <control typename="ICSSoft.STORMNET.Web.AjaxControls.FileControlView, ICSSoft.STORMNET.Web.AjaxControls" property="Value" codefile=""/>
    <editcontrol typename="ICSSoft.STORMNET.Web.AjaxControls.FileControl, ICSSoft.STORMNET.Web.AjaxControls" property="Value" codefile=""/>
  </propertytype>
<!-- ... -->
</root>
```

Также необходимо в `web.config` добавить следующие строки:

```xml
<configuration>
<!-- ... -->
<system.web>
    <!-- ... -->
    <httpHandlers>
      <!-- ... -->
      <add verb="POST" path="FileControlService.axd" type="ICSSoft.STORMNET.Web.HttpHandlers.FileControlHandler" validate="false" />
      <!-- ... -->
    </httpHandlers>
    <!-- ... -->
</system.web>
<system.webServer>
    <!-- ... -->
    <handlers>
      <!-- ... -->
      <add verb="POST" name="FileControlService" path="FileControlService.axd" type="ICSSoft.STORMNET.Web.HttpHandlers.FileControlHandler" resourceType="Unspecified" preCondition="integratedMode" />
      <!-- ... -->
    </handlers>
    <!-- ... -->
  </system.webServer>
</configuration>
```

Для сгенерированных "начисто" проектов данные настройки создаются автоматически.

## FileControl в WOLV
Контрол можно расположить в ячейках столбца WOLV в режиме ReadOnly (только возможность скачивания файла).

Необходимо указать, что для отображения типа File нужно использовать FileControl:

```xml
<customproperty class="BugReport" property="Attachment">
    <control typename="ICSSoft.STORMNET.Web.AjaxControls.FileControl, ICSSoft.STORMNET.Web.AjaxControls" property="Value" codefile=""/>
  </customproperty>
```

В WOLVSettApplyer.cs необходимо подписаться на событие WebControlProvider.TuneControlDelegateMethod, чтобы настроить свойство FileControl.ReadOnly = true для всех контролов FileControl, расположенных в WOLV:

```cs
wolv.WebControlProvider.TuneControlDelegateMethod += TuneControlDelegateMethod;

/// <summary>
/// Донастройка контролов в WOLV.
/// </summary>
/// <param name="control">Созданный контрол в WOLV.</param>
/// <param name="createdControlData">Информация о созданном контроле.</param>
private void TuneControlDelegateMethod(Control control, CreatedControlData createdControlData)
{
    // FileControl в WOLV должен быть в режиме "Только для чтения".
    var fileControl = control as FileControl;
    if (fileControl != null)
    {
        fileControl.ReadOnly = true;
        fileControl.EmptyFileNameText = string.Empty;
    }
}
```

## FileControl (Web) [JS API](fa_java-script-a-p-i.html)
*Раздел находится в процессе заполнения*
