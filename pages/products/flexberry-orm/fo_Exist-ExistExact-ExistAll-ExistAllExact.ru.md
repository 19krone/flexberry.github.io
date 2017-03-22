---
title: ExternalLangDef - ограничения на детейл (funcExist, funcExistExact, funcExistAll, funcExistAllExact)
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, Public, Ограничения
toc: true
permalink: ru/fo_exist--exist-exact--exist-all--exist-all-exact.html
---
* **Продукт**: [Flexberry ORM](fo_flexberry-orm.html)
* **Компонент**: [Компоненты для фильтрации и ограничения выборки получаемых данных](fo_limitation.html)
* **Программная библиотека**: ExternalLangDef.dll.
* **Предназначение**: Представлены основные функции [ExternalLangDef](fo_external-lang-def.html) для построения [ограничений](fo_limit-function.html) над детейлами.

## Описание и ключевые различия функций: funcExist, funcExistExact, funcExistAll, funcExistAllExact
При помощи этих функций [ExternalLangDef](fo_external-lang-def.html) возможно накладывать [ограничения](fo_limit-function.html) только на детейлы ([пример](fo_limit-details-by-agregators-prop.html))

| Название | Отображаемое название | Описание |
|---|---|---|
| funcExist | Существуют такие {}, что {} | Вернет True, если найдется хотя бы один объект, удовлетворяющий условию, в противном случае - False. Условие - только одна функция.|
| funcExistAll | Существуют все такие {}, что {} И {} И {} ... | Вернет True, если найдется хотя бы один объект, удовлетворяющий условию, в противном случае - False. В качестве условия могут выступать множество функций, которые автоматически соединятся конъюнкцией. Внимание! Допустимых видов функций только две: "=" ([FuncEQ](func-e-q.html)) и "СРЕДИ ЗНАЧЕНИЙ()" ([FuncIN](func-e-q.html)). |
| funcExistExact | Существуют только такие {}, что {} | Вернет True, если все объекты удовлетворяют условию, в противном случае - False. Условие - только одна функция. |
| funcExistAllExact | Существуют все только такие {}, что {} И {} И {} ... | Вернет True, если все объекты удовлетворяют условию, в противном случае - False. В качестве условия могут выступать множество функций, которые автоматически соединятся конъюнкцией. Внимание! Допустимых видов функций только две: "=" ([FuncEQ](func-e-q.html)) и "СРЕДИ ЗНАЧЕНИЙ()" ([FuncIN](func-e-q.html)). |

## Пример

![](/images/pages/img/Code Examples/Безымянный.jpg)

В следующем коде подразумевается, что в представлении `"СерверПодразделенияE"` обязательно присутствуют свойства `"Подразделение"` (так как оно есть в условии) и `"Сервер"` (свойство, по которому идет соединение).

Требуется вычитать те сервера, которые принадлежат определённому Подразделению (т.е. сервера, которые принадлежат и указанному Подразделению и еще какому-то, также будут вычитаны).

```cs
ExternalLangDef ldef = ExternalLangDef.LanguageDef;
LoadingCustomizationStruct lcsСервер = LoadingCustomizationStruct.GetSimpleStruct(typeof (Репликации.Сервер), "СерверE");
lcsСервер.LoadingTypes = new Type[] {typeof (Репликации.Сервер)};
View view = Information.GetView("СерверПодразделенияE", typeof(Репликации.СерверПодразделения));
ICSSoft.STORMNET.Windows.Forms.DetailVariableDef dvd = new ICSSoft.STORMNET.Windows.Forms.DetailVariableDef();
dvd.ConnectMasterPorp = "Сервер";
dvd.OwnerConnectProp = new string[] { SQLWhereLanguageDef.StormMainObjectKey };
dvd.View = view;
dvd.Type = ldef.GetObjectType("Details");
lcsСервер.LimitFunction = ldef.GetFunction(funcExist,
                                            dvd,
                                            ldef.GetFunction(ldef.funcEQ,
                                                            new VariableDef(ldef.GuidType, "Подразделение"),
                                                            UpdatedObject.НаправленоИз.__PrimaryKey));
lcsСервер.ReturnTop = 1;
ICSSoft.STORMNET.DataObject[] dobjsСервер = ICSSoft.STORMNET.Business.DataServiceProvider.DataService.LoadObjects(lcsСервер);
```

Требуется вычитать только те сервера, которые принадлежат только одному конкретному Подразделению (т.е. сервера, которые принадлежат и указанному Подразделению и еще какому-то, не будут вычитаны).

```cs
ExternalLangDef ldef = ICSSoft.STORMNET.Windows.Forms.ExternalLangDef.LanguageDef;
LoadingCustomizationStruct lcsСервер = LoadingCustomizationStruct.GetSimpleStruct(typeof (Сервер), "СерверE");
lcsСервер.LoadingTypes = new[] {typeof (Сервер)};
View view = Information.GetView("СерверПодразделенияE", typeof(Репликации.СерверПодразделения));
var dvd = new ICSSoft.STORMNET.Windows.Forms.DetailVariableDef
                {
                    ConnectMasterPorp = "Сервер",
                    OwnerConnectProp = new[] { SQLWhereLanguageDef.StormMainObjectKey },
                    View = view,
                    Type = ldef.GetObjectType("Details")
                };
lcsСервер.LimitFunction = ldef.GetFunction(funcExistExact,
                                            dvd,
                                            ldef.GetFunction(ldef.funcEQ,
                                                            new VariableDef(ldef.GuidType, "Подразделение"),
                                                            new Guid("6D7DC426-F5E9-4F63-B7B5-20C9E237DF2D")));
DataObject[] dobjsСервер = DataServiceProvider.DataService.LoadObjects(lcsСервер);
```
