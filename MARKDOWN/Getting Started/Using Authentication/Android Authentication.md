---
nav_sort: 4
src: /Getting Started/Using Authentication/Android Authentication.md
---

# Android Authentication

For any user to interact with GameSpark's platform they must be authenticated. There are three ways to authenticate to GameSparks:

* Username/Password
* Device Authentication
* Social Authentication

## Username/Password Authentication

Users can register to your game using a username and password. A user registers using the [RegistrationRequest](/API Documentation/Request API/Authentication/RegistrationRequest.md) and passing in string values for *DisplayName*, *UserName*, and *Password*:

```
    GSAndroidPlatform.gs().getRequestBuilder().createRegistrationRequest()
    .setUserName(string)
    .setDisplayName(string)
    .setPassword(string)
    .send(new GSEventConsumer<GSResponseBuilder.RegistrationResponse>() {
         @Override
         public void onEvent(GSResponseBuilder.RegistrationResponse registrationResponse) {
                if(!registrationResponse.hasErrors()){
                     //Do something
                   }
                  else{
                     //If there's an error
                     //Do something
                   }
                   }
          });

```

After a player is registered on the platform, they can use the [AuthenticationRequest](/API Documentation/Request API/Authentication/AuthenticationRequest.md) to login using the *UserName* and *Password*:

```

    //Authentication request through the GS request builder
    //The input is coming from editText widgets
    GSAndroidPlatform.gs().getRequestBuilder().createAuthenticationRequest()
    .setUserName(usernameTxt.getText().toString())
    .setPassword(passwordTxt.getText().toString())
    .send(new GSEventConsumer<GSResponseBuilder.AuthenticationResponse>()() {
            @Override
            public void onEvent(AuthenticationResponse authenticationResponse) {
                //Is the response error free?
                if(!authenticationResponse.hasErrors()){
                    //Do something
                }
                else{
                   //If there's an error
                   //Do something
                }
            }
            });

```


## Device Authentication

You can automatically authenticate devices by simply passing in a unique string device Id and string device OS. You can use this in combination with social authentication to keep track of your players:

```

GSAndroidPlatform.gs().getRequestBuilder().createDeviceAuthenticationRequest()
                    .setDeviceId(string).setDeviceOS(string).send(new GSEventConsumer<GSResponseBuilder.AuthenticationResponse>() {
                @Override
                public void onEvent(AuthenticationResponse authenticationResponse) {

                }
            });

```

### Social Authentication

Players can use their social accounts from a number of third party providers to create an account on the GameSparks platform. From March 2016 our third party providers currently are:
* Amazon
* Facebook
* Google Plus
* Google Play
* Game Center
* Steam
* Twitter
* XBOX Live
* Twitch
* Kongregate
* PSN
* Viber
* WeChat
* QQ

All social authentication requests follow a similar method of forwarding an authentication token to our platform. Here's an example of the Google Plus authentication request:

```
    GSAndroidPlatform.gs().getRequestBuilder().createGooglePlusConnectRequest()
                    .setAccessToken(String).setDoNotLinkToCurrentPlayer(Bool).send(new GSEventConsumer<GSResponseBuilder.AuthenticationResponse>() {
                @Override
                public void onEvent(AuthenticationResponse authenticationResponse) {

                }
            });

```

You can check out our API documentation site for the full list of requests, [here](/API Documentation/README.md).
