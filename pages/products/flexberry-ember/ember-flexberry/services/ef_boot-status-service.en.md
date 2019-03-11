--- 
title: Service application status 
sidebar: ember-flexberry_sidebar 
keywords: Flexberry Ember LockService 
toc: true 
permalink: en/ef_boot-status-service.html 
lang: en 
autotranslated: true 
hash: 5fb22bb0fcbb89465fdd59443329194cffb7ba50a676a6d93a3bc8d923704496 
summary: Methods of loading, success, error, warning, reset 
--- 

[Service download status](https://github.com/Flexberry/ember-flexberry/blob/master/addon/services/app-state.js) is a service through which you can control class for the upper forms in the application, this class uses [semantic](https://semantic-ui.com/collections/form.html) to display different States of form. 

The control is performed by specifying the appropriate method and class. 

Methods: 

* `loading` - controls the loading of the page 
* `success` - displays successful execution of operations 
* `error` - controls the display of errors 
* `warning` -controls the display of warning 
* `reset` - removes the established class 

### Example usage 

Submitted [example](https://github.com/Flexberry/ember-flexberry/blob/master/addon/services/app-state.js#L8) for `ember 3.x`. 

1.To add the service in app controller: 

```javascript
// app/controllers/application.js 
import Controller from '@ember/controller';
import { inject as service } from '@ember/service';
export default Controller.extend({
    appState: service(),
});
``` 

2.To register the state of the application in the template: 

```hbs
{% raw %}
<div class="ui {{appState.state}} form">
{{outlet}}
</div>
{% endraw %}
``` 

3.To use the service in the controller (component): 

```javascript
// app/controllers/my-controller.js 
import Controller from '@ember/controller';
import { inject as service } from '@ember/service';

export default Controller.extend({
    appState: service(),
    actions: {
        load() {
        this.get('appState').loading();
        this.load().finally(() => {
            this.get('appState').reset();
            });
        },
    },
});
``` 

In this instance, is the control page load, on successful completion of which the service deletes your settings. 



{% include callout.html content="Переведено сервисом «Яндекс.Переводчик» <http://translate.yandex.ru>" type="info" %}