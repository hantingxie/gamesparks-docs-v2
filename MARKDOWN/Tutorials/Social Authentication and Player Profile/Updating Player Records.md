---
nav_sort: 2
src: /Tutorials/Social Authentication and Player Profile/Updating Player Records.md
---

# Updating Player Records

## Introduction

After a player has been created, you might want to change details associated with the player's account such as:
* Password
* userName
* displayName

Different people might want to make a user account change:
* The game developer.
* One of the game's players.

Here, we'll learn how to make user account changes using the [ChangeUserDetailsRequest](/API Documentation/Request API/Player/ChangeUserDetailsRequest.md) in Cloud Code.  

## Change Details Request


This example shows an Event which takes a string input and sets it as the player's new *userName* using the *ChangeUserDetailsRequest* and outputs the response as scriptData.

```

//String input
//String input
Spark.getData().string

//Create an instance of the ChangeUserDetails request
var changeDetailsRequest = new SparkRequests.ChangeUserDetailsRequest();

//Set the userName. You can also change:
//Language / newPassword / oldPassword / displayName
changeDetailsRequest.userName = string;

//Send request and save response
var response = changeDetailsRequest.Send();

//Output response with scriptData
Spark.setScriptData("response", response);

```
