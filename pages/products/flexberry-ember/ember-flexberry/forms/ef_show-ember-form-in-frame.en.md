--- 
title: Display ember-shape without any additional elements 
sidebar: ember-flexberry_sidebar 
keywords: Flexberry Ember 
toc: true 
permalink: en/ef_show-ember-form-in-frame.html 
folder: products/ember-flexberry/forms/ 
lang: en 
autotranslated: true 
hash: 0c45193bcb037be9ce5aff1ca1b3c8af89048ea0d62e07196bd9b26cdceb655a 
summary: This feature enables you to display inside the frame exclusively ember-form without a menu and other additional elements. 
--- 

## Description 

If for some reason you want to display `голую` form (that is, without the site menu and other additional элементов; for example, inside the frame), you can use the following method: 

1. In the [controller `application.js`](ef_controller.html) ask [read parameter `inframe` Get-request](http://guides.emberjs.com/v2.4.0/routing/query-params/), create a property `shouldShowInFrame` that indicates that a specified parameter has a value `true`: 

```javascript
// ... 

export default Ember.Controller.extend({
  queryParams: {
    showinframe: 'inframe'
  },
  showinframe: null,
  shouldShowInFrame: function() {
    var inFrame = this.get('showinframe');
    return inFrame && inFrame.toLowerCase() === 'true';
  }.property('showinframe')
  
// ... 
});
``` 

2. In the template `application.hbs` with design `&#0123;&#0123;zgl[unless](http://guides.emberjs.com/v2.4.0/templates/conditionals/) shouldShowInFrame&#0125;&zgl0125; ... &#0123;&#0123;/unless&#0125;&zgl0125;` ask fragments that do not want to display on `голой` form. 

For example, lower left to display only the form itself, all other elements are hidden. 

```hbs
{% raw %}{{#unless shouldShowInFrame}}
	<div class="ui page grid menu">
	  <a class="brand item" href="#">Flexberry prototype written in Ember.js</a>
	  <div class="right menu">
		{{#if session.isAuthenticated}}
		  <div class="item">
			<i class="user icon"></i>
			{{session.secure.userName}}
		  </div>
			<a {{ action 'invalidateSession' }} class="item">Sign out</a>
		{{else}}
		  <div class="item">
			{{#link-to 'login' class="ui primary button"}}Sign in{{/link-to}}
		  </div>
		{{/if}}
	  </div>
	</div>
{{/unless}}
<div class="ui page grid">
	{{#unless shouldShowInFrame}}
	  <div class="four wide column">
		{{render "sitemap" sitemap}}
	  </div>
	{{/unless}}
  <div class="twelve wide column">
    {{outlet}}
		{{outlet 'modal'}}
  </div>
</div>{% endraw %}
``` 

3. When the form is to add a parameter `inframe=true`. 

{% include note.html content=" 
Important: 

* The implementation is not case-sensitive values `true`. 
* Implementation of the case-sensitive parameter `inframe`. 
* When passed as a value `inframe` values other than `true`, this logic will not work." 
%} 

![](/images/pages/img/page/ShowEmberFormInFrame/EmptyEmberForm.png) 

![](/images/pages/img/page/ShowEmberFormInFrame/FullEmberForm.png) 



 # Переведено сервисом «Яндекс.Переводчик» http://translate.yandex.ru/