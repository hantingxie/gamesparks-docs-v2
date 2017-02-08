---
nav_sort: 11
src: /Tutorials/Social Features/Setting Up Chat Messages.md
---

# Match Making Basics - Chat Messages

## Introduction

Once you match players together you will have reference to other player's PlayerIDs and account variables to use in Cloud Code and use of useful platform features. One of these features would be the exchange of messages. When you have a reference to the player's PlayerID you will be able to send them messages which are later intercepted using listeners.  

## Setup

To set up a chat message:

  1. Create an Event.
  2. Add a JSON Attribute. This will be used to store and access an array of string to use in the Cloud Code.
  3. Add a String Attribute. This will be used to store and access the message string.

![](img/MatchMessage/2.png)
 

### Cloud Code

This Cloud Code is simple, it takes the message passed in and sends it, together with the display name of sender, to the list of players passed in. To recreate it:

  1. Declare a variable which is set to the value of the array stored in the JSON attribute
  2. Declare a variable which is set to the value of the string attribute
  3. Declare a variable which is set to the display name of the sender (Current player)
  4. Declare a JSON with the first keypair value being the message variable and the second being the display name variable
  5. Using *Spark.sendMessageById(json, PlayerIDs)*, send the message to the list of players.



  ```    
    //JSON of Player IDs
    var ID= Spark.getData().Players;
    //Message string
    var chatString = Spark.getData().Message;
    //Sender displayName
    var dName = Spark.getPlayer().getDisplayName();

    //Group the display name and the message in one JSON
    var json = {"displayName":dName, "Message":chatString};

    //Send the message to all the players in the list
    Spark.sendMessageById(json, ID.pArray);
    ```

 

## Using the Event

To simulate an SDK we'll use the Test Harness to test our Event setup:

  1. Open three tabs, one for every player. Authenticate 3 players.
  2. For every player, call the [MatchmakingRequest](/API Documentation/Request API/Multiplayer/MatchmakingRequest.md) to match them up.
  3. Once all players are matched up and a matchID is returned, call the [MatchDetailsRequest](/API Documentation/Request API/Multiplayer/MatchDetailsRequest.md) using that matchID.
  4. Use the response to access the playerIDs (In a real SDK you'd use a loop) and copy them.
  5. Once you have the PlayerIDs, pass them into a [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md) (for the Event we made for the messages) through the JSON Attribute in a string array. Type a message in for the string Attribute and click send.
  6. After the request is sent, check the other player's tabs. You should see that those players have received orange messages. These orange messages are intercepted by using listeners on the SDKs and that's what you'll be looking to use to relay message to clients.
  7. Once the messages are received via a listener, access the 'Data' JSON variable which we sent through the *Spark.sendMessageByID()*. This JSON will include the message and any other variables passed through from cloud code.


#### Example request

```
    {
    "@class": ".LogEventRequest",
    "eventKey": "Chat_ToAll",
    "Players": {"pArray":["563b423ce4b0f85acff00a61",
    "563b4243e4b0f85acff00a69"]},
    "Message":"Hi!"
    }

```

#### Response

```
    {
    "@class": ".ScriptMessage",
    "messageId": "565f1bbce4b01ebee94e2e8c",
    "notification": true,
    "summary": "ScriptMessage",
    "data": {
    "displayName": "Dummy1",
    "Message": "Hi!"
    },
    "playerId": "563b423ce4b0f85acff00a61" //The receiving player's ID
    }

```
