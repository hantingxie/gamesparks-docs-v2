---
nav_sort: 5
src: /Tutorials/Cloud Code and the Test Harness/Using SparkRequests API to Send Requests in Cloud Code.md
---

# Sending Requests Using the SparkRequests API

SparkRequest API allows you to send GameSparks Requests from within Cloud Code.


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

## Simply Sending a Request or Sending and Executing Request Cloud Code

When you send a request using the SparkRequest API, you can:
* Simply send the request and not execute the Cloud Code attached to the request.
* Send the request and also execute the request's Cloud Code.

Here's an example of how to do this for an *AccountDetailsRequest*:

```
1
2 // Create Request
3 var req = new SparkRequests.AccountDetailsRequest();
4
5 // EITHER Send Request without executing Cloud Code
6 req.Send();
7
8 // OR Send Request and execute Cloud Code
9 req.Execute();
10
11


```

## Sending the Request and Grabbing the Response

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
