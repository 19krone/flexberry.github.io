---
title: Подсистема настроек
sidebar: product--sidebar
keywords: Flexberry Winforms
toc: true
permalink: ru/fw_setting-manager.html
folder: products/flexberry-winforms/
lang: ru
---

## Включение подсистемы настроек
Подсистема настроек предназначена для реализации сохранения пользовательских предпочтений в работе с приложением.


Доступ к системе настроек предоставляется менеджером настроек, набором статических методов класса `ICSSoft.STORMNET.Settings.SettingManager`.


Для того, чтобы включить подсистему настроек, необходимо установить статическое свойство `ICSSoft.STORMNET.Settings.SettingManager.UseSettings` в `true`. Также, можно это сделать в `config`-файле приложения, для чего необходимо добавить строку:
```xml
<add key="UseSettings" value="True"/>	
```
## Сохранение собственных настроек
Сохранение настроек выполняется функцией `SetSettings`, чтение настроек функцией `GetSetting`.


При сохранении настроек указывается:
# Имя модуля, для которого сохраняется настройка. Это просто некоторое логическое имя, позволяющее задавать группы настроек. Когда читается какая-либо настройка, на самом деле прочитываются и кешируются все настройки для модуля.
# Имя настройки.
# Значение настройки.
Настройка уникально идентифицируется по имени модуля, имени настройки и имени пользователя. Имя пользователя менеджер настроек берёт автоматически.


Пример (сохранение позиции и размера формы):

```

SettingManager.SetSetting("SettingsTest", "Form Position&Size", string.Join(",", new string[]{
					this.Left.ToString(),
					this.Top.ToString(),
					this.Width.ToString(),
					this.Height.ToString()
		}));
```

Пример (чтение позиции и размера формы):

```

	string setting = SettingManager.GetSetting("SettingsTest", "Form Position&Size");
	if (setting!=null)
	{
		string[] splittedsetting = setting.Split(',');
		this.Left=int.Parse(splittedsetting[0]);
		this.Top=int.Parse(splittedsetting[1](ис-управления-проектами_1.html));
		this.Width=int.Parse(splittedsetting[2]);
		this.Height=int.Parse(splittedsetting[3]);
	}
```

'''Важное замечание.''' Существует возможность представить любой объект в виде `XML`-строки используя стандартную `SOAP`-сериализацию `.NET`. Это делается утилитой `ICSSoft.STORMNET.Windows.Forms.Utils.ObjectToString` (обратное преобразование — `ObjectFromString`). Следовательно, можно не формировать вручную строку значения настройки, а воспользоваться этой утилитой.

Сериализация объектов данных выполняется другим образом: [Агрегирующие-функции|Как «закрутить» объект данных в строку XML и восстановить обратно]

'''Внимание: разработан новый [UserSettingsService](user-settings-service.html), призванный заменить `SettingManager`.'''
