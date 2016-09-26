---
nav_sort: 6
src: /SDK Center/JavaScript SDK.md
---

# JavaScript SDK Setup

The GameSparks JavaScript SDK allows you to interact with the GameSparks platform from any JavaScript environment.

## Getting the SDK

Download the SDK, and example HTML here:

[JavaScript SDK](http://repo.gamesparks.net/javascript-sdk/gamesparks-javascript-sdk-2015-12-18.zip)

</br>
<q>**Using Node JS to store Secret?** If you plan to use Node JS to store your API secret server-side see [this tutorial](/Tutorials/Third Party Integrations/Node JS Secret.md).

## Adding the SDK to your Web Page

There are two core JavaScript files included with the SDK:

* gamespark.js - The core SDK with connection management
* gamesparks-functions.js - An extension of the SDK to provide template functions for all GameSparks API methods. You may need to make your own extensions to the SDK for your custom events, this file will give you a template for achieving that.

To include the files in your HTML page, use the following script tags to reference the files.

```
    <script type="text/javascript" src="gamesparks.js"></script>
    <script type="text/javascript" src="gamesparks-functions.js"></script>
```

The example application also uses a script to perform HMAC SHA-256 operations on the SDK for security.

```
    <script type="text/javascript" src="hmac-sha256.js"></script>
```

This is used for the example project, but it is assumed you will secure the secret on your own server.

## Initialising the SDK

There are two initialization methods in the SDK, one for using the preview servers (for your internal use and testing) and another for the live players. It's important that you don't try to use the preview servers for your live players because the preview servers have a limit of 50 concurrent connections for each game.

Firstly, you need to create a GameSparks object:

```
    //Create a gamesparks object to be used
    var gamesparks = new GameSparks();
```

Once you have an object reference, you can initialize the SDK. To do this, you need to call one of the initialization methods with an options object. To initialize against the preview servers use the following function:

```
    gamesparks.initPreview({
     key:<YOUR API KEY>,
     onNonce: <HMAC FUNCTION>,
     onInit:<INITIALISATION CALLBACK>,
     onMessage:<ASYNC MESSAGE HANDLER>,
     });
```

To initialize against the live servers use the following function:

```
    gamesparks.initLive({
     key:<YOUR API KEY>,
     onNonce: <HMAC FUNCTION>,
     onInit:<INITIALISATION CALLBACK>,
     onMessage:<ASYNC MESSAGE HANDLER>,
     });
```

### Initialization options

*key* : The API Key of your game from the GameSparks developer portal.

*onNonce* : A JavaScript function that takes a string and returns an SHA-256 HMAC of the string using your secret. A simple example below:

```
    //Callback function to hmac sha256 a nonce with the secret. It's assumed you will have your own method of securing the secret;
    function onNonce(nonce){
    	return CryptoJS.enc.Base64.stringify(CryptoJS.HmacSHA256(nonce, <YOU API SECRET>));
    }
```

*onInit* : A JavaScript function that is called when the SDK is finished initialising. You can use this function to perform a common task, such as authenticating the user when the SDK is ready.

```
    //Callback to handle when the SDK is initialized and ready to go
    function onInit(){
    	console.log("Initialized");
    }
```

*onMessage* : A JavaScript function that takes a JS Object that was sent to the client asynchronously. This function is called whenever a Message object is sent from the server to the client.

```
    //Callback to handle async messages from the gamesparks platform
    function onMessage(message){
    	console.log(JSON.stringify(message));
    }
```

## Sending requests to GameSparks

A number of helper methods exist in the gamesparks object to allow you to make requests. See gamesparks-functions.js for details of each.

A method exists for each GameSparks request object, with each of the parameters required in the request as function arguments.

Each method take a callback function as the final parameter to be called when the response is received from the GameSparks platform. This function should take a single object parameter. A basic authentication example is shown below.

```
    gamesparks.authenticationRequest("testuser", "testuser", loginResponse);

    function loginResponse(response){
    	console.log(JSON.stringify(response));
    }
```

Custom requests, which allow you to post events to the GameSparks platform can be achieved by using the sendWithData method. See the example below for sending a LogEventRequest for an Event with shortCode "FIRST_EVENT" and 3 attributes "NUMBER_ATTR", "STRING_ATTR" and "JSON_ATTR"

```
    gamesparks.sendWithData("LogEventRequest",
        {
            eventKey : "FIRST_EVENT",
            NUMBER_ATTR : 123,
            STRING_ATTR : "this is a string",
            JSON_ATTR : {key1 : 12, key2 : "abc"}
        },
        function(response){console.log(JSON.stringify(response);}
    );
```
