---
title: Запуск мобильного приложения 
keywords: Mobile, Phone, Cordova, tablet, Android, iOS, App, AppStore, play market
sidebar: guide-mobile-app_sidebar
toc: false
permalink: ru/gma_launch-mobile-app.html
lang: ru
---

## Описание

На данном шаге описан процесс запуска мобильных приложений Android и iOS на разлиных устройствах, для тестирования работоспособности разработанных приложений.

## Запуск мобильного приложения Android

Запустить созданое приложение для мобильных устройств в Apache Cordova можно 3 различными способами, представлеными ниже.

### На эмуляторе устройства

Для запуска приложение на эмуляторе устройства в командной строке выполните команду `cordova emulate android`, при выполнение данной команды происходит сборка и запуск мобильного приложения.

![](/images/pages/guides/mobile-app/cordova-emulate-android.png)
![](/images/pages/guides/mobile-app/cordova-emulate-android1.png)

{% include note.html content="Если после запуска эмулятора, не произошел запуск приложения, тогда в командной строке выполните команду cordova run android." %}

![](/images/pages/guides/mobile-app/cordova-run-mobile-app.png)

### На подключеном к компьютеру телефоне

Для запуска мобильного приложения на телефоне в командной строке выполните команду `cordova run android`.

![](/images/pages/guides/mobile-app/cordova-run-mobile-app2.png)

{% include note.html content="Если Cordova не обнаружить подключенного к компьютеру телефона, запуск приложения будет произведен на эмуляторе устройства." %}

### В приложение Android Studio 

Открывем и запускам приложения через [Android Studio](https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html#opening-a-project-in-android-studio).

В результате выполения данного шага был описан процесс запуска мобильных приложений. Далее будет представлены статьи о том как опубликовать созданное приложение в AppStore или Google Play.

## Вы можете

* [Перейти на следующий шаг ->](gma_publish-mobile-app.html)
* [<- Вернутся на предыдущий шаг](gma_build-mobile-app.html)