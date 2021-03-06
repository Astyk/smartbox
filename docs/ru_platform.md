# Platform

Базовый класс через который вызываются нативные методы устройства. Вы можете расширить его и добавить свою новую платформу. После `SB.ready` текущая платформа уже определена и хранится в `SB.currentPlatform`.

###Оглавление

<a href="#Публичные-свойства">`Публичные свойства`</a>
* <a href="#sbcurrentplatformkeys">`SB.currentPlatform.keys`</a>
* <a href="#sbcurrentplatformduid">`SB.currentPlatform.DUID`</a>
* <a href="#sbconfigduid">`SB.config.DUID`</a>
* <a href="#sbcurrentplatformname">`SB.currentPlatform.name`</a>
* 
<a href="#Публичные-методы">`Публичные методы`</a>
* <a href="#detect">`detect`</a>


<a href="#Добавление-новой-платформы">`Добавление новой платформы`</a>
 
##Публичные свойства

###`SB.Platform.platformUserAgent`

*String*: строка используемая для детектирования платформы с помощью `userAgent`.

```js
SB.currentPlatform.keys.TOOLS; //=> 32
```


###`SB.currentPlatform.keys`

*Plain object*: хеш, содержащий коды клавиш и их названия. 

```js
SB.currentPlatform.keys.TOOLS; //=> 32
```


###`SB.currentPlatform.DUID`

*String*: содержит уникальный ID устройства

###`SB.currentPlatform.DUID`

*String*: содержит уникальный ID устройства

###`SB.config.DUID` 

*String*: настройка которая показывает каким способом приложение будет получать DUID. Значение по умолчанию: `real`.

`real`: используется метод SB.Platform.getNativeDUID()

`mac`: используется метод MAC адрес устройства, доступно для LG и Samsung,

`random`: при каждом запуске приложения будет сгенерирован новый DUID

`[Другое значение]`: будет использовано в качестве DUID. Например: 

```js
SB.config.DUID="fgsfds";
SB.ready(function(){
  SB.currentPlatform.DUID;//=> "fgsfds"
});
```


##Публичные методы


###detect

Определяет платформу. По умолчанию ищет строку `SB.Platrorm.platformUserAgent` в `navigator.userAgent`. 

#### Возвращает

*Boolean*: `true` при успешном детекте и `false` при не успешном.


###`SB.currentPlatform.name`

*String*: название платформы (samsung, lg, philips, etc...)


##Добавление новой платформы

Вы можете добавить новую платформу, создавая объект `SB.Platform`. 

Далее, если вы хотите использовать определениче через `userAgent` нужно переопределить свойство `platformUserAgent`. Если какой-то другой способ, то нужно переопределить метод `detect` и вернуть `true`, если окружение удовлетворяет каким-то условиям.

```js
  var platform = new SB.Platform('philips'),
    platformObj;

  platformObj = {
    platformUserAgent: 'nettv',
    detect: function(){
      return !!window.opera;
    }
    //TODO: override some methods
  };
  
  _.extend(platform, platformObj);
```
