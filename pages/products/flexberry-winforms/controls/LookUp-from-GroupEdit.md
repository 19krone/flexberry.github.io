---
title: Поднятие из GroupEdit'a на лукап объекта, не имеющего ссылку на объект-инициатор
sidebar: product--sidebar
keywords: Windows UI (Контролы)
toc: true
permalink: ru/look-up-from--group-edit.html
folder: product--folder
lang: ru
---

# Поднятие из GroupEdit'a на лукап объекта, не имеющего ссылку на объект-инициатор

На __примере__ поднятия '''Дежурной группы''' из GE "Дежурные группы смены" на форме Дежурной смены из поля "Номер группы":

Есть класс '''ДежурнаяГруппаСмены''' и не связанный с ним (отношениями ассоциации или композиции) класс '''ДежурнаяГруппа'''. По лукапу номера группы нужно вызвать список ДежурныхГрупп для заполнения полей ДежурнойГруппыСмены из свойств выбранной ДежурнойГруппы.

Для этого:

1. В методе '''GetControl''' класса CustomControlProvide устанавливаем контрол для поля НомерГруппы:

```
            if (view.Name #  "ДежурнаяГруппаСменыE" && propertyName  "НомерГруппы")
            {
                ICSSoft.STORMNET.Windows.Forms.LookUp lookUp = new ICSSoft.STORMNET.Windows.Forms.LookUp();

                ctrl = new ICSSoft.STORMNET.Windows.Forms.Binders.ControlForBindStruct(lookUp, "Value");
            }```
2. Переопределяем метод '''OnEdit''' в winformДежурнаяСменаE. Так как класс ДежурнаяГруппаСмены не имеет ссылки на ДежурнуюГруппу, то выбираем любой другой класс, имеющий такую ссылку, в нашем случае подойдет '''ЧленДежурнойГруппы'''.

То есть пишем :

```
dataobject = new ЧленДежурнойГруппы(); //класс, имеющий ссылку на дежурную группу
propertyname = "ДежураяГруппа"; //имя ссылки

public override void OnEdit(string propertyname, ICSSoft.STORMNET.DataObject dataobject, string contpath, object tag)
        {
            if (dataobject is ДежурнаяГруппаСмены && propertyname == "ДежурныеГруппыСмены.НомерГруппы")
            {
                if (((ДежурнаяГруппаСмены)dataobject).ТипДежурнойГруппы != null)
                {
                    SQLWhereLanguageDef langdef = new SQLWhereLanguageDef();
                    tag = langdef.GetFunction(langdef.funcEQ,
                            new VariableDef(langdef.GuidType, "ТипДежурнойГруппы"), ((ДежурнаяГруппаСмены)dataobject).ТипДежурнойГруппы.__PrimaryKey);
                }
                dataobject = new ЧленДежурнойГруппы();
                propertyname = "ДежураяГруппа";
            }

            base.OnEdit(propertyname, dataobject, contpath, tag);
        }```

3. Переопределяем метод '''Edited''' в winformДежурнаяСменаE. Записываем все необходимые свойства в ДежурнуюГруппуСмены из выбранной ДежурнойГруппы:

```
public override void Edited(ICSSoft.STORMNET.DataObject dataobject, string contpath, string propertyname)
        {
            base.Edited(dataobject, contpath, propertyname);

            if (dataobject is ЧленДежурнойГруппы && propertyname == "ДежураяГруппа")
            {
                ДежурнаяГруппаСмены ДежГрСмены = (ДежурнаяГруппаСмены)ДежурныеГруппыСмены.EditManager.DataObject;
                ДежурнаяГруппа ДежГр = ((ЧленДежурнойГруппы)dataobject).ДежураяГруппа;
                ICSSoft.STORMNET.Business.DataServiceProvider.DataService.LoadObject("ДежурнаяГруппаE", ДежГр);
                ДежГрСмены.НомерГруппы = ДежГр.НомерГруппы;
                ДежГрСмены.ТипДежурнойГруппы = ДежГр.ТипДежурнойГруппы;
                ДежГрСмены.Руководитель = ДежГр.Руководитель;
                ДежГрСмены.Комментарий = ДежГр.Комментарий;
                ДежГрСмены.Позывной = ДежГр.Позывной;
                ДежГрСмены.ЧленыДежГруппыСмены.Clear();

                for (int t = 0; t < ДежГр.ЧленыДежурнойГруппы.Count; t++)
                {
                    Объекты.ЧленДежурнойГруппы членДежГр = ДежГр.ЧленыДежурнойГруппы[t];
                    Объекты.ЧленДежГруппыСмены чдгс = new Объекты.ЧленДежГруппыСмены();
                    чдгс.ДежурнаяГруппаСмены = ДежГрСмены;
                    чдгс.НомерПП = членДежГр.НомерПП;
                    чдгс.Сотрудник = членДежГр.Сотрудник;
                    чдгс.Позывной = членДежГр.Позывной;
                    ДежГрСмены.ЧленыДежГруппыСмены.Add(чдгс);
                }
                ДежурныеГруппыСмены.EditManager.Change();
            }
        }```
 

