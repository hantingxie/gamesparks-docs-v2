---
nav_sort: 10
src: /Documentation/Configurator/Cloud Code.md
---

# Cloud Code

The *Configurator > Cloud Code* page lists all the potential interception points that Cloud Code can be bound to, and has a JavaScript editor where you can write your
interception code.

The *Bindings* section is split into ten sub-categories, which are further explained in the sections below.

![](img/CloudCode/5.png)

To access the Cloud Code JavaScript editor select the name of the script from one of the ten drop down menus in the *Bindings* section.  Use the *Delete*, *Close*, and *Save* buttons at the bottom of the editor to manage your scripts:

![](img/CloudCode/16.png)

<q>**Keyboard Shortcuts to Save!** You can also save your scripts using standard key press combinations, **CMD+S** on OSX and **CTRL+S** on Windows and Linux.</q>

<q>**Keyboard Shortcuts List!** For a list of keyboard shortcuts that you can use in the Cloud Code Editor see [below](#Cloud Code Editor Keyboard Shortcuts)</q>

## Events

![](img/CloudCode/6.png)

The *Events* list contains an entry for each Event you have created within the GameSparks platform:
* When a [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md) is received, the corresponding script is executed allowing you to run custom code on the platform. For more details, see [Events](/Documentation/Configurator/Events.md).
* You can access the current player making the request using *Spark.getPlayer()*.
* You can quickly create a new Event by clicking the plus ![](/img/fa/plus.png) icon. This opens the same *Create Event* dialog as opened from the [Events](/Documentation/Configurator/Events.md) page.

## Challenge Events

![](img/CloudCode/6.png)

The *Challenge Events* list contains an entry for each Event you have created within the GameSparks platform:
* When a [LogChallengeEventRequest](/API Documentation/Request API/Multiplayer/LogChallengeEventRequest.md) is received, the corresponding script is executed allowing you to run custom code on the platform.
* *LogChallengeEventRequest* contains an attribute "challengeId". It's useful to get this value for keying your own data and to access the value you can call *Spark.data.challengeId*. To get the challenge object stored within GameSparks the following call should be executed:

```    
    var myChallenge = Spark.getChallenge(Spark.data.challengeId);
```

* You can also access the current player making the request using *Spark.getPlayer()*.
* You can quickly create a new Event by clicking the plus ![](/img/fa/plus.png) icon. See the Events section above for details.

## Requests

![](img/CloudCode/8.png)

The *Requests* list contains an entry for each Request you can call within the GameSparks platform:
* When a Request is received, the corresponding script is executed allowing you to run custom code on the platform.
* You can access the current player making the request using *Spark.getPlayer()*.

<q>**Adding Common Functionaltiy!** [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md) and [LogChallengeEventRequest](/API Documentation/Request API/Multiplayer/LogChallengeEventRequest.md) are global scripts that will be executed for these request types before a specific script is called for each Event. This allows you to add a common functionality to all Events.</q>

## Responses

![](img/CloudCode/9.png)

The *Responses* list contains an entry for each Response that can be returned from the GameSparks platform:
* When a Response is created, the corresponding script is executed before sending it to the player allowing you to run custom code on the platform.
* You can access the current player who has generated the response using *Spark.getPlayer()*.

## User Messages

![](img/CloudCode/10.png)

The *User Messages* list contains an entry for each Message that can be returned from the GameSparks platform:
* Before a Message is sent out to each player within a Challenge, the corresponding script is executed allowing you to run custom code on the platform.
* You can access the current player who has generated the response using *Spark.getPlayer()*.

## Global Messages

![](img/CloudCode/11.png)

The *Global Messages* list contains an entry for each Message that can be returned from the GameSparks platform:
* When a Message is created the corresponding script is executed allowing you to run custom code on the platform.
* You **cannot access** the current player in a global message Cloud Code script.

## Modules

![](img/CloudCode/12.png)

Modules allow you to create your own libraries of JavaScript that can be included within other scripts. This allows you to separate common functionality that needs to be shared between scripts into a single module that can be included.

* To include a module within your script use the *require* method as follow :

```
    require("MODULE_SHORT_CODE");
```

* Using *require*, you can load a module into the current execution context. This is not common.js require, but a more basic inclusion pattern, where the loaded module is inlined within the current script.
* If you have circular reference between modules, the *require* method will only load a single module once per *require* invocation. This is to protect from infinite loops and stack overflows.
* You can conditionally *require* modules based on input parameters and the like, to have a single script that can perform multiple tasks without having a large script:

```    
    if(something) {
        require("MODULE_SHORT_CODE_1");
    } else {
        require("MODULE_SHORT_CODE_2");
    }

```

* To create a new module, click the plus ![](/img/fa/plus.png) icon. Then, on the *Create Module* dialog, enter a *Short Code* to uniquely identify the new module script.

## Callbacks

![](img/CloudCode/13.png)


* *Callbacks* contains an item for each custom *Credential* created:
* Separate [Callback URLs](/Tutorials/Cloud Code and the Test Harness/Using Custom Callback Urls.md) allow users to assign different Cloud Code scripts to different callbacks for the same game.


## Realtime Scripts

![](img/CloudCode/14.png)

*Realtime Scripts* are listed here:
* You can link Realtime scripts to a Match configuration in the Multiplayer Section so that when a Match is found, the arbitrary Cloud Code script that communicates with the Real-Time client is triggered.
* To create a new Realtime script, click the plus ![](/img/fa/plus.png) icon.
* For more details on Realtime Services, see [here](/Tutorials/Real-Time Services/README.md).

## System

![](img/CloudCode/15.png)

The *System* tab contains a number of System Events that are able to trigger some JavaScript Cloud Code:

  * *Callback Url* - This script is executed whenever something hits the [Callback Url](/Tutorials/Cloud Code and the Test Harness/Implementing External HTTP Callbacks.md).
  * *Every Day* - This script is executed at 12:00am UTC each day.
  * *Every Hour* - This script is executed on the hour, every hour.
  * *Every Minute* - This script is executed on the minute, every minute.
  * *File Delivered* - This script is executed when a file is delivered via SFTP to the GameSparks platform. SFTP access to the GameSparks platform is available on request. Please raise a support ticket to request this.
  * *Game Published* - This script is executed when your game configuration changes:
    * On the Preview stage this script will be executed each time you save your game within the portal, you should track your own internal version number in Preview if this script is performing potentially dangerous operation.
    * On the Live stage, this script is executed once each time you publish your game.
  * *Player Connected* - This script is executed each time a player connects and is identified. *Spark.getPlayer()* is set to be the player who connected so you can query or manipulate the data related to the player.
  * *Player Disconnected* - This script is executed each time a player disconnects. *Spark.getPlayer()* is set to be the player who disconnected so you can query or manipulate the data related to the player.

## Cloud Code Editor Keyboard Shortcuts

This section lists keyboard shortcuts you can use when working in the Cloud Code Editor.

### Selection

| Windows/Linux | Mac | Action              
| ------| --------- | ---------
|  Ctrl+A | Command+A | Select All
|  Shift+Left | Command+Left | Select Left
|  Shift+Right | Command+Right | Select Right
|  Ctrl+Shift+Left | Option+Shift+Left | Select Word Left
|  Ctrl+Shift+Right | Option+Shift+Right | Select Word Right
|  Shift+Home | Shift+Home | Select Line Start
|  Shift+End | Shift+End | Select Line End
|  Alt+Shift+Left | Command+Shift+Left | Select to Line Start
|  Alt+Shift+Right | Command+Shift+Right | Select to Line End
|  Shift+Up | Shift+Up | Select Up
|  Shift+Down | Shift+Down | Select Down
|  Ctrl+Shift+Home | Command+Shift+Up | Select to Start
|  Ctrl+Shift+End | Command+Shift+Down | Select to End
|  Ctrl+Shift+D | Command+Shift+D | Duplicate Selection

### Line Operation

| Windows/Linux | Mac | Action              
| ------| --------- | ---------
|  Ctrl+D | Command+D | Remove Line
|  Alt+Shift+Down | Command+Option+Down | Copy Lines Down
|  Alt+Shift+Up | Command+Option+Up | Copy Lines Up
|  Alt+Down | Option+Down | Move Lines Down
|  Alt+Up | Option+Up | Move Lines Up
|  Alt+Delete | Ctrl+K | Remove to Line End
|  Alt+Backspace | Command+Backspace | Remove to Line Start
|  Ctrl+Backspace | Option+Backspace, Ctrl+Option+Backspace | Remove Word Left
|  Ctrl+Delete | Option+Delete | Remove Word Right
|  --- | Ctrl+O | Split Line
|  Ctrl+M+/ | --- | Comment/Uncomment Line


### Go To

| Windows/Linux | Mac | Action              
| ------| --------- | ---------
|  Ctrl+L, Ctrl+M+L | Command+L, Command+M+L | Go to Line
|  Left | Left, Ctrl+B | Go to Left
|  Right | Right, Ctrl+F | Go to Right
|  Ctrl+Left | Option+Left | Go to Word Left
|  Ctrl+Right | Option+Right | Go to Word Right
|  Up | Up, Ctrl+P | Go to Line Up
|  Down | Down, Ctrl+N | Go to Line Down
|  Alt+Left, Home | Command+Left, Home, Ctrl+A | Go to Line Start
|  Alt+Right, End | Command+Right, End, Ctrl+E | Go to Line End
|  Ctrl+Home | Command+Home, Command+Up | Go to Start
|  Ctrl+End | Command+End, Command+Down | Go to End
|  Ctrl+Down | Command+Down | Scroll Line Down
|  Ctrl+Up | --- | Scroll Line Up


### Find/Replace

| Windows/Linux | Mac | Action              
| ------| --------- | ---------
|  Ctrl+F, Ctrl+M+F | Command+F | Find
|  Ctrl+H | Command+Option+F | Replace
|  Ctrl+K,| Command+G | Find Next
|  Ctrl+Shift+K | Command+Shift+G | Find Previous
