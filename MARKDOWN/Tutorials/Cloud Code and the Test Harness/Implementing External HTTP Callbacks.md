---
nav_sort: 8
src: /Tutorials/Cloud Code and the Test Harness/Implementing External HTTP Callbacks.md
---

# How to Implement External HTTP Callbacks

You can make HTTP calls into the GameSparks platform either from external servers or from your own processes. When these calls are made, you can execute some custom Cloud Code to do whatever processing you need:
* The HTTP request can either be a GET or POST request, and all parameters passed to the server are accessible via the [Spark.getData()](/API Documentation/Cloud Code API/Spark.md) function.
* If you pass query string parameters on a POST request, both sets of values are accessible:
  * Single parameters are passed to JavaScript as Strings.
  * Multiple parameters with the same name are passed to JavaScript as a String array.
* POST parameters are only interpreted into the data object when the content type of the request is "multipart/form-data". For other usages see the [Reading POST Data](#Reading POST Data) section below.

## Creating Cloud Code to Handle Requests

To create a script to handle the request from the Cloud Code page, under *Scripts* select *System*, and use *Callback URL*.

## The Callback URL

*https: //{stage}.gamesparks.net/callback/{apiKey}/{serverSecret}/{playerId}*

  * *stage* : "preview" or "service" (depending on whether you are accessing the live servers or not).
  * *apiKey* : The API Key of you game.
  * *serverSecret* : The server secret of you game, accessible from the *Configurator > Credentials* page.
  * *playerId(optional)* : The ID of the player. If this is supplied, then [Spark.getPlayer()](/API Documentation/Cloud Code API/Spark.md) will be the player specified.


## Adding Parameters

For a *GET* request, you can add parameters to the query string that are passed to your script. For example:

*https: //{stage}.gamesparks.net/callback/{apiKey}/{serverSecret}/{playerId}?attr1=abc&attr2=bcd&attr2=cde*

With this URL, the following code can be used to access these parameters:

```

    //attribute1 is a string
    var attribute1 = Spark.getData().attr1;

    //attribute2 is an array
    var attribute2 = Spark.getData().attr2;

    //attribute2[0] is bcd
    //attribute2[1] is cde

```

## Producing Output

The scriptData object from the callback script is written to the output stream as a JSON document.

```   

    Spark.setScriptData("key1", "value1");
    Spark.setScriptData("key2", "value2");

```
This will generate the JSON output:

```

    {
        "key1": "value1",
        "key2": "value2"
    }

```

If you do not want to write JSON but want to use your own text based output, setting a value with the key "RESPONSE_RAW" in script data will override the JSON output and return this value directly;

```

    Spark.setScriptData("RESPONSE_RAW", "OK");

```

Will generate the response as :

```

    OK

```

## Reading POST Data

There are instances where a remote server may not set the content-type header correctly, and the post data are not automatically translated into *Spark.getData()*. In these cases, the POST requests have an additional "REQUEST_BODY" attribute set into *Spark.getData()*. This is the body of the HTTP post request as a string, so you can do your own parsing of this value:

```  
    var rawPostData = Spark.getData().REQUEST_BODY

```
