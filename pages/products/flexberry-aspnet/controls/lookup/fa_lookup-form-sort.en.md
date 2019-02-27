--- 
title: Sorting in list form, raised on lucapa 
sidebar: flexberry-aspnet_sidebar 
keywords: Web UI (Controls) 
toc: true 
permalink: en/fa_lookup-form-sort.html 
lang: en 
autotranslated: true 
hash: 0e49e2c405a21c6cb035b4c019d543e8967c6039639604f7f1a9854c1f294140 
--- 

In order to be able to sort in list form, [raised lucapa web](fa_lookup-overview.html), you must do the following: 

1.You need to make sure that the LookUp form is correct. For example, to use the standard user form located on the test stand, then the settings in `web.config` shall be as follows: 

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
	...
  <httpHandlers>
	...
      <add verb="*" path="LookUpForm.aspx" type="ICSSoft.STORMNET.Web.AjaxControls.HandlerFactories.PageHandlersFactory`1[[ICSSoft.STORMNET.Web.Controls.LookUpForm, TestStand(ASP.NET Application)]], ICSSoft.STORMNET.Web.AjaxControls" validate="false" />
  </system.web>
  <system.webServer>
    <handlers>
		...
      <add name="LookUpForm" path="LookUpForm.aspx" verb="*" type="ICSSoft.STORMNET.Web.AjaxControls.HandlerFactories.PageHandlersFactory`1[[ICSSoft.STORMNET.Web.Controls.LookUpForm, TestStand(ASP.NET Application)]], ICSSoft.STORMNET.Web.AjaxControls" resourceType="Unspecified" preCondition="integratedMode" />
    </handlers>
  </system.webServer>
</configuration>
``` 

2.To check that the form method is used ApplyWolvSettings [WOLVSettApplyer](fa_wolv-sett-applyer.html) application availability (not located in the Assembly AjaxControls) and that no calls to the base method ApplyWolvSettings (this call can grind settings). 

```cs
namespace ICSSoft.STORMNET.Web.Controls
{
    /// <summary> 
    /// Class applied forms of lyapov. 
    /// </summary> 
    public class LookUpForm : AjaxControls.Forms.LookUpForm
    {
        /// <summary> 
        /// Apply the settings to wolv lying on the form lucapa. 
        /// Overridden method implements the application logic of the adjustments WOLV on the form. 
        /// </summary> 
        protected override void ApplyWolvSettings()
        {
            new WOLVSettApplyer().SettingsApply(LookUpFormWOLV);
        }
    }
}
``` 

3.In [WOLVSettApplyer](fa_wolv-sett-applyer.html) override method `ApplyLookUpSettings`. And assign the necessary [operation](fa_wolv-operations.html). 

```csharp
namespace ICSSoft.STORMNET.Web
{
    /// <summary> 
    /// The tuner for WOLV'and available for application programmers. 
    /// </summary> 
    public class WOLVSettApplyer : AjaxControls.WolvSettApplyer
    {
        /// <summary> 
        /// Apply settings for WOLV in the form of lucapa. Called if the HTTP request 
        /// there is a parameter <see cref="P:ICSSoft.STORMNET.Web.Tools.WebParamController.OpenedFromLookupParamName"/>. 
        /// </summary> 
        /// <param name="wolv">WOLV to which you want the settings to apply.</param> 
        public override void ApplyLookUpSettings(WebObjectListView wolv)
        {
            base.ApplyLookUpSettings(wolv);
            Type[] dataObjectTypes = wolv.DataObjectTypes;
            if (wolv.ID.Equals(LookUpForm.WebObjectListViewID)) // Impose the desired condition. 
            {
                wolv.Operations.UserColumnsSort = true;
            }
        }
    }
}
``` 



 # Переведено сервисом «Яндекс.Переводчик» http://translate.yandex.ru/