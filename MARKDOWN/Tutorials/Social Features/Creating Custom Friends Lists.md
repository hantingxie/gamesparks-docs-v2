---
nav_sort: 14
src: /Tutorials/Social Features/Creating Custom Friends Lists.md
---

# Creating Custom Friends Lists

## Introduction

In this tutorial, we're going to build a very simple system for creating your own friends lists so your players can search for friends, send their friends invites, and get information about their current friends for use in Challenges or chat later on in your game.

## Creating a Player List

Before we can start searching for players to add to our list we need to be able to get a collection of player information we can query so that we can filter our search requests. In this example, we'll be storing some of the important player information in this player list so we can search for user-names, countries, and so on.
Therfore to start, we'll create a new player-doc each time a player registers with GameSparks and we'll do this in the [RegistrationResponse](/API Documentation/Request API/Authentication/RegistrationRequest.md) script.

*1.* Go to *Configurator>Cloud Code*.

*2.* In the *Scripts* panel, select the *Responses* folder.

*3.* Open *RegistrationResponse* and add the following Cloud Code:

![](img/FriendsList/1A.png)


For the moment, we'll only put the player’s ID, user name, and display name in this script. In the next section, we'll add data to this so users can update it:

```
if(Spark.getData().error === undefined)
{
    Spark.runtimeCollection("playerList").insert(
        {
            "playerId" : Spark.getPlayer().getPlayerId(),
            "displayName" : Spark.getPlayer().getDisplayName(),
            "userName" : Spark.getPlayer().getUserName(),
        });
}


```

### Testing

To test this, we can go to the Test Harness and register a new player:

![](img/FriendsList/2.png)


When the player has been registered, we can see a new entry for this player in the *playerList* collection in the *NoSQL Explorer* tab. Select the collection and click *Find* to see the documents in this collection.

![](img/FriendsList/3.png)

## Adding More Information to Players

Next, we'll create a request so that we can add information to our player-documents. Others can then use those details to search for us.

In this example, we'll add some Attributes like country, city, and level to the Event. However, you can add other Attributes you think your players might want to search for.

To create a new Event:

*1.* Go to *Configurattor>Events*.

*2.* Click the *Add* button.

In this example, we'll call the Event *updatePlayerInfo* because we're not only going add information here, but we can also update existing information (like display name or user-name).

<q>**Player's ID is not Updated!** Note that we'll never edit the player’s ID. This is our link back to the player’s GameSparks account and it's important that the *playerId* always remains the same.</q>

![](img/FriendsList/4.png)

Notice that we've given each of these Attributes a *Default Value*. This allows you to leave out the Attributes you don’t want to update. For instance, if you later wish to only update the value for the *username* Attribute, then you can just use that Attribute in the request. We’ll see an example of this later.

Now that the *updatePlayerInfo* Event has been created, we need to open it up in the Cloud Code editor and start updating the player docs:

*1.* Go to *Configurator>Cloud Code*.

*2.* In the *Scripts* panel, select the *Events* folder.

*3.* Open *updatePlayerInfo* and add the following Cloud Code:

![](img/FriendsList/5.png)

Here's the script:

```
if(Spark.getData().userName != "null")
{
    Spark.runtimeCollection("playerList").update({ "playerId" : Spark.getPlayer().getPlayerId() }, { $set : { "userName" : Spark.getData().userName } });
}

if(Spark.getData().displayName != "null")
{
    Spark.runtimeCollection("playerList").update({ "playerId" : Spark.getPlayer().getPlayerId() }, { $set : { "displayName" : Spark.getData().displayName } });
}

if(Spark.getData().country != "null")
{
    Spark.runtimeCollection("playerList").update({ "playerId" : Spark.getPlayer().getPlayerId() }, { $set : { "country" : Spark.getData().country } });
}

if(Spark.getData().city != "null")
{
    Spark.runtimeCollection("playerList").update({ "playerId" : Spark.getPlayer().getPlayerId() }, { $set : { "city" : Spark.getData().city } });
}

if(Spark.getData().level != -1)
{
    Spark.runtimeCollection("playerList").update({ "playerId" : Spark.getPlayer().getPlayerId() }, { $set : { "level" : Spark.getData().level } });
}


```

### Testing

We can test this through the Test-Harness. For this example, we'll only add info about my *country*, *city*, and *level*, excluding *userName* and *displayName*. You'll notice that the code above will ignore these fields because their values are null, while it will update everything else:

![](img/FriendsList/6.png)

Now, if we go to the *NoSQL Explorer* we'll see those fields updated in the player’s doc:

![](img/FriendsList/7.png)

So now that players can be searched for and we can load players using the playerId, we are ready to make our search Events.

## Searching for Friends

We need to create an Event which will allow us to search for available players that we can send friend requests to. We'll create the *findPlayers* Event for this, which will have one JSON Attribute. The JSON Attribute will act as the query we'll search for:

![](img/FriendsList/8.png)

In the script that we attach to this Event, we're going to add some code to find all the players matching the query and return them. Later on, we'll use the *playerIds* from this request to send friend invites:

![](img/FriendsList/9.png)

```
var query = Spark.getData().query;
// we want to make sure this player isnt returned in the list //
query["playerId"] = { "$ne" :  Spark.getPlayer().getPlayerId() };
var results = Spark.runtimeCollection("playerList").find(query);
Spark.setScriptData("playerList", results);


```

We are also including another query in this code, to make sure that we don’t include ourselves in the player-search. So we use the *$ne* (not-equals) operator to exclude ourselves for the search.

### Testing

At the moment, we only have one player registered, so we're going to have to register a few more players and add information to their documents in order for this to work properly. Once you have some new players registered, we can test this out in the Test Harness. The query field we're going to use here is just the field we want to check and the value we want to search for.

For example, if we know our friend’s *userName* or *displayName*, then we put that in directly:

![](img/FriendsList/10.png)

You could also perform a Regex query to find players with names containing a letter or word using the “$regex” operator:

![](img/FriendsList/11.png)

This will also work for *level* or *city*. Just play around with the query to find out how you might want to use it. You could also add more complexity to this request, such as returning a limited number of players or filtering out the player data for privacy reasons.

## Creating Friend Requests

So now that we can get a list of players, it’s time to invite those players to our list of friends. We're going to use another collection for this called *playerFriends*. The process of inviting will have several steps:
1.	We need to check to see if the friend has declined a previous request. We'll track this in the *playerFriends* collection.
2.	We send a message to the player and create a log in *playerFriends* to track that we’ve a pending friend request with that player.

So we'll need to create a new [ScriptMessage](/API Documentation/Message API/Misc/ScriptMessage.md) and a new Event.

The message is going to be very simple. It’ll have a default title and message, and we’ll use the Short Code to send it from our Event.

To create a new *ScriptMessage*:

*1.* Go to the *Configurator>Messages* and select the *ScriptMessage Extensions* tab.

*2.* Click *Add*.

*3.* In the *Add Message* page, configure a new *friendRequestMessage*:

![](img/FriendsList/12.png)

Don’t worry too much about this message at the moment because we'll be setting our data for it later.

Next, we need to create the *friendRequest* Event. We'll add 3 Attributes to this Event:
* The most important Attribute is the *player_id* - for the friend we are inviting.
* We'll also add a *group* Attribute - so we can group our friends by family, work, college, and so on.
* Finally, we're going to add a *message* Attribute - to allow us to send a custom message to the player we want to invite.

![](img/FriendsList/34.png)

Notice that we've entered *Default Values* for the *group* and *message* Attributes. This is because we shouldn’t require these to send a friend request. We can leave these out and just send the basic template of the message.

### Cloud Code

We've discussed what the Cloud Code for this request is going to look like earlier, so the request will appear as follows:

![](img/FriendsList/14.png)

Here's the full script:

```
var playerId = Spark.getData().player_id;
var group = Spark.getData().group;
var message = Spark.getData().message;
// now we check the pending requests to see if the player has declined a previous request //
var declinedCheck = Spark.runtimeCollection("playerFriends").findOne({ "status" : "declined", "friendId" : playerId, "playerId" : Spark.getPlayer().getPlayerId() });
if(!declinedCheck)
{
    // this is the data we want to track on the pending request //
    var requestData = {
        "playerId" :  Spark.getPlayer().getPlayerId(),
        "displayName" : Spark.loadPlayer(playerId).getDisplayName(),
        "friendId" : playerId,
        "group" : group,
        "status" : "pending"
    };
    // then we update the friend list to show that we have a pending friend-request //
    Spark.runtimeCollection("playerFriends").insert(requestData);

    // if we havent been blocked then we send a message //
    var newMessage = Spark.message("friendRequestMessage");
    newMessage.setPlayerIds(playerId);
    newMessage.setMessageData({
        "message" : message,
        "requestId" : requestData._id.$oid,
        "senderId" : Spark.getPlayer().getPlayerId(),
        "displayName" : Spark.getPlayer().getDisplayName()

    });
    newMessage.send();

    // and return a script message to show that the request was completed successfully //
    Spark.setScriptData("success", "request-sent")
}
else // if a request has already been declined then send back an error
{
    Spark.setScriptError("errorCode", "player-declined")
}

```

### Testing

To test this out, we need to log two players in through the Test Harness. You can get the *player_id* for the player you want to send the request to using the *findPlayers* request. Once you have the player selected, fill in the details of the *friendRequest*:

![](img/FriendsList/15.png)

Once you send the request:
* You should see that the other player has received a message:

![](img/FriendsList/16.png)

* You should also see that there is a new document in the *playerFriends* collection, with this request marked as "pending". We'll use the *requestId* from the message above to either accept or decline the friend request:

![](img/FriendsList/17.png)

## Accepting and Declining Requests

### Accepting Requests

Accepting the friends request is pretty straightforward. We simply need to create a new *acceptFriendRequest* Event which will take the *requestId* from the request we just sent to the other player. They'll use this Event to accept the friend request:

![](img/FriendsList/18.png)

In the Cloud Code for this Event, we want to check that the *requestId* is valid, and, if so, we'll update the document in the *playerFriends* collection to say that the request has been accepted. This friend’s details will then show up in the players list of friends (which we'll create an Event for later).

We also want to send a message to the player who sent the friend request to tell them that their request has been accepted. In this example, we created another [ScriptMessage](/API Documentation/Message API/Misc/ScriptMessage.md) with a simple template. There's no need to add extra data to this message because it just needs to say the request was accepted. If you need to add extra data, you can do so in the way that we did with the previous message:

![](img/FriendsList/19.png)

Here's the script:

```
var requestId = Spark.getData().request_id;
var request = Spark.runtimeCollection("playerFriends").findOne({ "_id" : { "$oid" : requestId }, "status" : "pending" });
if(request)
{
    // if the request is valid then we update the friend-list to say there that this friend accepted the request
    Spark.runtimeCollection("playerFriends").update({ "_id" : { "$oid" : requestId }},{ $set : { "status" : "accepted" }});
    // and send a message to the original player //
    var newMessage = Spark.message("friendAcceptedMessage");
    newMessage.setPlayerIds(request.friendId);
    newMessage.send();
}
else
{
    // we return an error to say there was an invalid request id //
    Spark.setScriptData("errorCode", "invalid-request-id")
}


```
#### Testing

Now that we have this request created, we can log back into the Test Harness and get the *requestId* for the friend request we sent in the last section:

![](img/FriendsList/20.png)


* You'll see that a message is sent to the original player too:

![](img/FriendsList/22.png)

* You'll also see that the document in the *playerFriends* collection has been updated to ‘accepted’:

![](img/FriendsList/21.png)

### Declining Friend Requests

Declining a friend request works in a similar way as accepting a friend request. We'll create a new *declineFriendRequest* Event for it, which will take the *requestId*. We also need to create a new [ScriptMessage](/API Documentation/Message API/Misc/ScriptMessage.md), so we have a template for declined request messages:

![](img/FriendsList/23.png)

The Cloud Code for this Event is identical to the accepted request, except  that we set the status of the request to “declined” and send out the *friendRequestDeclined* message instead:

![](img/FriendsList/24.png)

Here's the script:

```
var requestId = Spark.getData().request_id;
var request = Spark.runtimeCollection("playerFriends").findOne({ "_id" : { "$oid" : requestId }, "status" : "pending" });
if(request)
{
    // if the request is valid then we update the friend-list to say there that this friend declined the request
    Spark.runtimeCollection("playerFriends").update({ "_id" : { "$oid" : requestId }},{ $set : { "status" : "declined" }});
    // and send a message to the original player //
    var newMessage = Spark.message("friendRequestDeclined");
    newMessage.setPlayerIds(request.playerId);
    newMessage.send();
}
else
{
    // we return an error to say there was an invalid request id //
    Spark.setScriptData("errorCode", "invalid-request-id")
}

```

#### Testing

We can use the same setup as we did for accepting requests to test declining requests. All we need is a *requestId* we want to decline:

![](img/FriendsList/25.png)

* You'll see the declined message appear for the original sender:

![](img/FriendsList/26.png)

You can also test that this player cannot send any more requests because our *friendRequest* Event checks to see if there are any declined requests before allowing the player to send new requests:

![](img/FriendsList/27.png)

## Getting a Player's Friends List

Next, we need to create a way for players to see a list of all their friends. So we'll create an Event called *getPlayerFriends*. This Event is going to have an Attribute for selecting which group we want to search for, which will default to *all* if we want to return all friends:

![](img/FriendsList/28.png)

The Cloud Code for this Event will be very simple. We'll just query the *playerFriends* collection for friends matching the group requested and return all the friends we find. In this example, we only need to return the *playerId* and *displayName*, so we'll filter the results to only include this data:

![](img/FriendsList/29.png)

Here's the script:

```
var group = Spark.getData().group;
var friendsCursor;
if(group === "all")
{
    var friendsCursor = Spark.runtimeCollection("playerFriends").find({ "playerId" : Spark.getPlayer().getPlayerId(), "status" : "accepted"  });
}
else
{
    var friendsCursor = Spark.runtimeCollection("playerFriends").find({ "playerId" : Spark.getPlayer().getPlayerId(), "status" : "accepted", "group" : group  });
}
// once we have the cursor, we want to take some data out of the doc because we only need the name and playerId //
var friendsList = [];
while ( friendsCursor.hasNext())
{
   var friend =  friendsCursor.next();
   friendsList.push({
       "friendId" : friend.friendId,
       "displayName" : friend.displayName

   });
}
Spark.setScriptData("friendsList", friendsList);


```

### Testing

We can test this Event using the Test Harness, as we’ve done before. If we use the *Default Value* of *all* for the *group* Attribute, we should see all of your friends returned:

![](img/FriendsList/30.png)

For the following example, we’ve added a group Attribute for *family* into the *getPlayerFriends* requests, so we can also test that this returns specific groups:

![](img/FriendsList/31.png)

## Player Online Message

The last thing we are going to do is implement a system for notifying players when their friends come online. This is going to require a new [ScriptMessage](/API Documentation/Message API/Misc/ScriptMessage.md) and in this case we'll use a system-script instead of creating a new Event.

GameSparks already has a script that runs when the player comes online which we can use in this case.

*1.* Go to *Configurator>Cloud Code*.

*2.* In the *Scripts* panel, select the *System* folder.

*3.* Open *PlayerConnected* and add the following Cloud Code:

![](img/FriendsList/32.png)

Here's the Cloud Code for *PlayerConnected*:

```
// get my friends list
var playerFriends = Spark.runtimeCollection("playerFriends").find({ "playerId" : Spark.getPlayer().getPlayerId(), "status" : "accepted" });
// go through all the friends so we can send messages //
while (playerFriends.hasNext())
{
   var friend = playerFriends.next();
   // next we check if our friends are online currently //
   if(Spark.loadPlayer(friend.friendId).isOnline())
   {
       // send friend online message //
       var newMessage = Spark.message("friendOnlineMessage");
        newMessage.setPlayerIds(friend.friendId);
        newMessage.setMessageData({
            "senderId" : Spark.getPlayer().getPlayerId(),
            "displayName" : Spark.getPlayer().getDisplayName()
        });
        newMessage.send();
   }
}


```

### Testing

To test this, all we need is to login through the Test Harness with two players.

To show that the message is being correctly sent:

*1.* Authenticate a first player and keep them logged on.

*2.* Authenticate a second player - you should see that the first player gets a message through the Test Harness if the first player is on the second player's friends list:

![](img/FriendsList/33.png)

## Additional Options or Features

This tutorial implements a very basic set of features to send and receive friend requests and to get a player's list of friends. There's wide scope for additional functionality. For example, you can:

* Add a player's information from the *playerList* collection to the list of data returned when you get your friends. This would allow you to include things like avatars or other personal information about your friends to your game.
* You can also allow friends to use privacy options to check which details they want you to have access to, or how they appear when you search for them.

The important thing is that, once you have the friends list, you have access to the *playerId* of any of you friends. You can then use this *playerId* throughout the GameSparks APIs to set up Events, Matches, Challenges, or Teams to include your friends.

Try it out for yourself and contact our Customer Support or the forums if you need any help in implementing specific features regarding your players' friends in GameSparks!
