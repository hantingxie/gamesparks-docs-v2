---
nav_sort: 4
src: /Tutorials/Cloud Code and the Test Harness/Sending Requests in Cloud Code.md
---

# Using the SparkRequests API

SparkRequest API allows you to send GameSparks Requests from within Cloud Code.

Cloud code bound to these requests and responses are not executed when sent using this API. If you want to execute cloud code on the requests and responses you can do this by modularising your code and executing the same module before sending the request and after receiving the response. This restriction is in place to protect from infinite loops that could occur. You can see how this works [here](/Documentation/Key Concepts/Cloud Code.md).

## Creating a Request

The Request object can be easily created using the following notation:

```
1
2 var authenticationRequest = new SparkRequests.AuthenticationRequest();
3

```

## Setting Request Parameters

All of the parameters that are available for the particular Request, can be set using the following notation:

```

1
2 authenticationRequest.userName = "username";
3 authenticationRequest.password = "password";
4

```

## Sending the Request and grabbing the Response

There are a few ways to dispatch the request and they primarily differ by who the request is sent by:


```

1
2 // Send the request as currently Authenticated player and save the response JSON
3 var authenticationResponse = Spark.sendRequest(authenticationRequest);
4 // OR
5 var authenticationResponse = authenticationRequest.Send();
6
7 // Send the request as the player who's Id was provided and save the response JSON
8 var authenticationResponse = Spark.sendRequestAs(authenticationRequest, playerId);
9 // OR
10  var authenticationResponse = authenticationRequest.SendAs(playerId);
11

```


## The Response data

The Response is a JSON object that can be easily queried, here’s an example:

```
1
2 var authenticationResponse = Spark.sendRequest(authenticationRequest);
3
4 if(authenticationResponse.error != null){
5   // Do something
6 }
7

```
