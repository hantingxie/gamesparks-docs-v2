---
nav_sort: 7
src: /Tutorials/Cloud Code and the Test Harness/Changing Player Passwords.md
---

# How to Change Player Passwords

If your game uses the [RegistrationRequest](/API Documentation/Request API/Authentication/RegistrationRequest.md) GameSparks API method for signing up players to your game, you might want to enable them to change their password in the future.

This tutorial describes two possible ways to achieve this:
* Using the [ChangeUserDetailsRequest](/API Documentation/Request API/Player/ChangeUserDetailsRequest.md) API method.
* Using the [SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md) Cloud Code object.

## Changing Passwords with ChangeUserDetailsRequest API call

The [ChangeUserDetailsRequest](/API Documentation/Request API/Player/ChangeUserDetailsRequest.md) call contains a 'newPassword' field, which you can use to alter the currently authenticated player's details.

Let's try this out using the GameSparks developer portal Test Harness.

*1.* In the GameSparks portal, navigate to the *Test Harness*.

*2.* Copy the JSON request below into the JSON field and click the *Send* ![](/img/fa/play.png) icon.

```    
    {
     "@class": ".RegistrationRequest",
     "userName": "nick",
     "password": "password1",
     "displayName": "Nick"
    }

```

The GameSparks platform will return a response similar to this.

```    
    {
     "@class": ".RegistrationResponse",
     "authToken": "a8c88571-31c5-4747-adb7-34f04bcd1bf4",
     "displayName": "Nick"
     "scriptData": null,
     "userId": "537f755d4566a1b7eb012e92"
    }

```  

This player is now authenticated and could sign into later sessions using these credentials with an [AuthenticationRequest](/API Documentation/Request API/Authentication/AuthenticationRequest.md).

If you want to change this player's password to a new one, you make a [ChangeUserDetailsRequest](/API Documentation/Request API/Player/ChangeUserDetailsRequest.md) call that provides the new password in the 'newPassword' field.

*3.* In the Test Harness, copy the JSON request below into the JSON field and press the *Send* ![](/img/fa/play.png) icon.

```

    {
     "@class": ".ChangeUserDetailsRequest",
     "newPassword": "password2"
    }

```

The GameSparks platform will return a response similar to this:

```

    {
     "@class": ".ChangeUserDetailsResponse",
     "scriptData": null
    }

```

For greater security, you might require that the player enters their existing password along with the new one - the *ChangeUserDetailsRequest* call allows you to provide the old password which the GameSparks platform will verify before changing it to the new value.

*4.* In the Test Harness, copy the JSON request below into the JSON field and press the *Send* ![](/img/fa/play.png) icon.

```    
    {
     "@class": ".ChangeUserDetailsRequest",
     "oldPassword": "password2",
     "newPassword": "password3"
    }

```
The GameSparks platform will return a registration response similar to this:

```

    {
     "@class": ".ChangeUserDetailsResponse",
     "scriptData": null
    }

```

## Changing Passwords via Cloud Code

First of all, we need to create an Event which the game client code will use to post a password change request into the GameSparks platform. We'll be attaching a Cloud Code script to this Event later on.

*1.* In the GameSparks developer portal navigate to *Configurator > Events*.

*2.* Click the plus icon Plus ![](/img/fa/play.png) icon to add a new Event. Enter the following details:

![](img/PassChange/1.jpg)

*3.* Now navigate to *Configurator > Cloud Code > Bindings > Events*.

*4.* Select the *Change Password* item to open up the Javascript editor for the Cloud Code associated with this Event:

![](img/PassChange/2.jpg)

*5.* Copy the following script to the editor and click the *Save* button:

```    
    var oldPassword = Spark.getData().OLD_PASS;
    var result = Spark.getPlayer().validatePassword(oldPassword);

    if (result) {
     var newPassword = Spark.getData().NEW_PASS;
     Spark.getPlayer().setPassword(newPassword);
    } else {
     Spark.setScriptData("result", "Incorrect existing password");
    }

```

This script reads the old password from the incoming Event, validates it against the password currently stored for this player and, if they match, changes the password to the value specified in the incoming Event.

Let's test out this configuration in the *Test Harness*.

*1.* First authenticate with the previously created player.

*2.* Copy the JSON request below into the JSON field and press the *Send* ![](/img/fa/play.png) icon.

```  

    {
     "@class": ".AuthenticationRequest",
     "userName": "Nick",
     "password": "password"
    }

  ```  

The GameSparks platform will return a registration response similar to this:

```

    {
     "@class": ".AuthenticationResponse",
     "authToken": "1c53797a-6e3f-4db7-b529-b70820c35303",
     "displayName": "displayName",
     "scriptData": null,
     "userId": "53808a96e4b02eeeac89e23a"
    }

```

*3.* Now send the [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md) containing the current password and the new one. The GameSparks platform will intercept this request and execute the Cloud Code script that we provided to validate and change the player's password.

```   

    {
     "@class": ".LogEventRequest",
     "eventKey": "PASSWORD",
     "OLD_PASS": "password",
     "NEW_PASS": "mynewp4ssword"
    }

```

The GameSparks platform will return a registration response similar to this:

```

    {
     "@class": ".LogEventResponse",
     "scriptData": null
    }

```
