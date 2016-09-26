---
nav_sort: 3
src: /Getting Started/Using Cloud Code/Android Cloud Code.md
---

# Android Cloud Code

## Introduction

In this tutorial, we'll follow two examples of using Cloud Code when using Android with the GameSparks platform:
* Log Event Requests.
* Requests and Responses for extra functionality.

## Android Log Event Requests

You can create your own custom Events in the Android SDK that are called through the GamesSparks request builder. Events can have 3 types of input:
* String
* Number
* JSON

<q>**Note:** The JSON object can hold floats, booleans, strings, numbers, arrays, and other objects.</q>

<q>**More Details?** For more details about how to work with Events, go to the [Events](/Documentation/Configurator/Events.md) page.</q>

In this tutorial, we'll build an example using a *set* and a *get* Event:
* Call them *setDetails* and *getDetails*.
* *setDetails* will have 3 attributes:
  * *Name* and *Gender* which will be strings.
  * *Age* which will be a number.
* The *setDetails* Event will save scriptData against our player's database.
* The *getDetails* Event will find the scriptData and retrieve it to the SDK.

### setDetails Event

*1.* In the portal, go to *Configurator > Cloud Code > Events* and create the *setDetails* Event with the 3 attributes given above.

*2.* Select the *setDetails* Event and in the Cloud Code editor, add the following Cloud Code:

```
    //Declare variables and set them from input
    var pName = Spark.getData().name;
    var pAge = Spark.getData().age;
    var pGender = Spark.getData().gender;

    //Save these values against the player
    Spark.getPlayer().setScriptData("name", pName);
    Spark.getPlayer().setScriptData("age", pAge);
    Spark.getPlayer().setScriptData("gender", pGender);

```
Here:
* *Spark.getData()* retrieves the data associated with the request, including the attributes passed in from the SDK. Since the data is an object, you can easily retain the data inside it through a variable name.
* *getPlayer().setScriptData(name,value)* will save a value under a specific name in the scriptData object which can easily be accessed and is viewable in any response that returns the player's data - for example the *AccountDetails* request.

<q>**Alternative?** Optionally, you can use *setPrivateData()* to store the data in the player's privateData, which is not present with any response unless called for and returned specifically. For more information, see [Storing Custom Player Data](/Tutorials/Cloud Code and the Test Harness/Storing Custom Player Data.md).</q>

*3.* To call this request from the SDK and pass in the values, you can use the Event Key to reference the correct Event ShortCode.

```
GSAndroidPlatform.gs().getRequestBuilder().createLogEventRequest().setEventKey("setDetails")
                            .setStringEventAttribute("name", string)
                            .setNumberEventAttribute("age", int)
                            .setStringEventAttribute("gender", string).send(new GSEventConsumer() {
                        @Override
                        public void onEvent(GSResponseBuilder.LogEventResponse logEventResponse) {
                            if(logEventResponse.hasErrors()){
                                //DO something
                            }
                            else{
                                //Do something
                            }
                        }
                    });

```

This example does not cover passing in objects. But to do that:

```
    Map scriptData = new HashMap();

            scriptData.put("Key", 21);
            scriptData.put("AnotherKey", "This String");
            scriptData.put("Yet Another",true);

```
### getDetails Event

The *getDetails* event won't have any attributes and will return the values that we saved against the player's scriptData.

Here's the Cloud Code:

```

//Retrieve data saved against the player
    var pName = Spark.getPlayer().getScriptData("name")
    var pAge = Spark.getPlayer().getScriptData("age")
    var pGender = Spark.getPlayer().getScriptData("gender")

//Return it as scriptData
    Spark.setScriptData("name", pName);
    Spark.setScriptData("age", pAge);
    Spark.setScriptData("gender", pGender);

    Here's how to retrieve the scriptData from the SDK:

    GSAndroidPlatform.gs().getRequestBuilder().createLogEventRequest()
                    .setEventKey("getDetails").send(new GSEventConsumer() {
            @Override
            public void onEvent(GSResponseBuilder.LogEventResponse logEventResponse) {
                if(logEventResponse.getScriptData().getAttribute("name") != null){/*Do something*/}
                if(logEventResponse.getScriptData().getAttribute("age") != null){/*Do something*/}
                if(logEventResponse.getScriptData().getAttribute("gender") != null){/*Do something*/}
            }
            });
```

<q>**The Basic Method!** This example using a combination of Events and Cloud Code illustrates the basic method of passing and returning values from SDK to the GameSparks platform.</q>

## Android Requests and Responses Extra Functionality

GameSparks conveniently offers you the ability to augment existing calls and responses with extra functionality. In the portal, if you navigate to *Configurator > Cloud Code*, you will see tabs for Requests, Responses, User Messages, and Global Messages. Once expanded, these tabs will allow you to add Cloud Code to any request, response, or message and achieve the extra functionality you want in your game.

In this tutorial, we'll follow an example of how to do this by adding Cloud Code to the Registration request and response so that:
* The *RegistrationRequest* will be blocked if the email is not passed in.
* The *RegistrationResponse* will get the registered player's email and save it against that player's scriptData.

Lastly, we'll see how to add scriptData to requests from the SDK for Android clients.

### Registration Request

First, we'll navigate to *Configurator > Cloud Code > Requests* and open the Registration Request Cloud Code. In there we'll add:

```
if(!Spark.getData().scriptData){
    Spark.setScriptError("Error", "Need an Email")
} else{
    Spark.setScriptData("email",Spark.getData().scriptData.email );
}

```

This will ensure that if the value 'email' isn't passed in through the scriptData object, then the registration will not continue.


### Registration Response

Second, we'll navigate to *Configurator > Cloud Code > Responses* and add this to the Cloud Code:

```
if(Spark.getData().scriptData){
    var email = Spark.getData().scriptData.email;
    Spark.getPlayer().setScriptData("email", email);
}

```

After the response is received, the player will be authenticated, so calling *Spark.getPlayer()* will return the just registered player. After getting the player, we save the email value against their scriptData.

### SDK Request

Finally, here's how we add scriptData to your requests from the SDK, similar to the way we use Attributes for Events:

```

Map scriptData = new HashMap();
    scriptData.put("email",string);

    GSAndroidPlatform.gs().getRequestBuilder().createRegistrationRequest()
          .setUserName(string)
          .setDisplayName(string)
          .setPassword(string)
          .setScriptData(scriptData)
          .send(new GSEventConsumer() {
            @Override
            public void onEvent(GSResponseBuilder.RegistrationResponse registrationResponse) {

                  }
            });

```
