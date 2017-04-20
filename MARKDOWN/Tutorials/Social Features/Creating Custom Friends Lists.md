---
nav_sort: 14
src: /Tutorials/Social Features/Creating Custom Friends Lists.md
---

# Creating Custom Friends Lists

## Introduction

In this tutorial, we're going to build a very simple system for creating your own friends lists so your players can search for friends, send their friends invites, and get information about their current friends for use in challenges or chat later on in your game.

## Creating a Player List

Before we can start searching for players to add to our list we need to be able to get a collection of player information we can query so that we can filter our search requests. In this example, we'll be storing some of the important player information in this player list so we can search for user-names, countries, and so on.
To start, we'll create a new player-doc each time a player registers with GameSparks. We will do this in the [RegistrationResponse](/API Documentation/Request API/Authentication/RegistrationRequest.md) script.

You can find the *RegistrationResponse* script by going to the *Configurator>Cloud Code* tabs and choosing the Cloud-Code menu. You will then find the script under *Responses*:

![](img/FriendsList/1.png)


All we'll put in this script for the moment will be the player’s ID, user name, and display name. In the next section we will add data to this so users can update it:

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

To test this, we can go the Test Harness and register a new player:

![](img/FriendsList/2.png)


Once the player has been registered we can see a new entry for this player in the playerList collection in the NoSQL explorer tab. Once you have the collection selected, click on the Find button to see the documents in this collection.

![](img/FriendsList/3.png)

## Adding More Information to Players

Next we'll create a request so that we can add information to our player-documents so that others can use those details to search for us.

In this example, we'll use some set-fields like country, city, and level. However, you can add other fields you think your players might want to search for.

To create a new Event:

*1.* Go to *Configurattor>Events*.

*2.* Click the *Add* button.

In this example, we'll call the Event *updatePlayerInfo* because we're not only going add info here, but we can also update existing info (like display name or user-name).

<q>**Player's ID is not Updated!** Note that we'll never edit the player’s ID. This our link back to the player’s GameSparks account and it's important that the *playerId* always remains the same.</q>

![](img/FriendsList/4.png)

Notice that we've added default values for these fields. This allows you to leave out the fields you don’t want to update. For instance, if you later wish to only update the username field, then you can just use that attribute in the request. We’ll see an example of this later.

Now that the *updatePlayerInfo* Event has been created, we need to open it up in the Cloud Code editor and start updating the player docs - go to *Configurator>Cloud Code* and you'll find the Event under *Scripts>Events*:

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

We cannot test this through the Test-Harness. For this example I am only going to add info about my level, city and country, excluding userName and displayName. You will notice that the code above will ignore these fields as their values are null, while it will update everything else.


Now, if we go to the NoSQL explorer we will see those fields updated in the player’s doc.

So now that players can be searched for and we can load players using the playerId, we are ready to make our search events.

## Searching for Friends

We need to create an event that will allow us to search for available players we can send friend requests to. We will create an event for this which will have one JSON field. The JSON field will act as the query we will search for.

In this script we are just going to add some code to find all the players matching the query and return them. Later on we will use the playerIds from this request to send friend invites.



We are also including another query in this code, to make sure that we don’t include ourselves in the player-search. So we use the not-equals operator to exclude ourselves for the search.

### Testing

At the moment we only have one player registered, so we are going to have to register a few more players and add information to their documents in order for this to work properly. Once you have some new players we can test this out in the Test-Harness. The query field we are going to use here is just the field we want to check and the value we want to search for.
For example, if we know our friend’s userName or displayName, then we put that in directly…

You could also perform a Regex query to find players with names containing a letter or word using the “$regex” operator.

And of course it works for level or city too. Just play around with the query to find out how you might want to use it. You could also add more complexity to this request, like returning a limited number of players, or filtering out the player data for privacy reasons.

## Creating Friend Requests

So now that we can get a list of players it’s time to invite those players to our list of friends. We are going to use another collection for this called playerFriends. The process of inviting is going to have several steps.
1.	We need to check to see if the friend has declined a previous request. We will track this in the playerFriends collection.
2.	We send a message to the player and create a log in playerFriends to track that we’ve a pending friend request with that player.
So we will need to create a new ScriptMessage, and a new event.
The message is going to be very simple. It’ll have a default title and message, and we’ll use the short code to send it from our event. To create a new ScriptMessage, go to the Configurator tabs and select ‘Messages’ from menu. You will them see a tab called ‘ScriptMessage Extensions’.

Don’t worry too much about this message at the moment as we will be setting our data for it later.
Next we need to create the friendRequest event. This event is going to have 3 attributes. The most important is going to be the playerId (for the friend we are inviting) and we will also add a group field (so we can group our friends by family, work, college, etc). And finally we are going to add a message field which will allow us to send a custom message to the player we want to invite.

Notice that I have also added default values to the group and message attributes. This is because we shouldn’t require these to send a friend request. We can leave these out and just send the basic template of the message.

### Cloud Code

We have discussed what the cloud-code for this request is going to look like earlier, so the request will appear as follows.

### Testing

So to test this out we need to log two players in through the Test-Harness. You can get the playerId for the player you want to send the request to using the findPlayers request. Once you have the player selected, fill in the details of the freindRequest.





















Once you send the request, you should see that the other player has received a message.

And that there is a new document in the playerFriends collection, with this request marked as ‘pending’. We will use the requestId from the message above to either accept or decline the friend request.


## Accepting and Declining Requests

Accepting the friends request is pretty straight forward. We just need to create a new event which will take the requestId from the request we just sent to the other player.
They will use this event, to accept the friend request.

In the cloud-code for this event, we want to check that the requestId is valid, and if so, we will update the document in the playerFriends collection to say that the request has been accepted. This friend’s details will then show up in the players list of friends (which we will create an event for later).
We also want to send a message to the player who sent the friend request to tell them that their request has been accepted. In this example I created another ScriptMessage with a simple template. There is no need to add extra data to this message as it just needs to say the request was accepted. If you need to add extra data, you can do so like we did with the previous message.










### Testing

Now that we have this request created, we can log back into the Test-Harness and get the requestId for the friend request we sent in the last section.

You will see that a message is sent to the original player too.

And that the document in the playerFriends collection has been updated to ‘accepted’.

### Declining Friend Requests

Declining a friend request works mostly the same as accepting. We will create a new event for it, which will take the requestId. We also need to create a new ScriptMessage so we have a template for declined request messages.

And the cloud-code for this event is identical to the accepted request, only that we set the status of the request to “declined” and sent out the friendRequestDeclined message instead.



### Testing

We can use the same setup as we did for accepting request to test declining requests. All we need is a requestId we want to decline.

And you will see the declined message appear for the original sender.

You can also test that this player cannot send any more requests, as our friendRequest event checks to see if there are any declined requests before allow the player to send new requests.


## Getting a Player's Friends List

Next we need to create a way for players to see a list of all their friends. So we will create and event called getPlayerFriends. This event is going to have an attribute for selecting which group we want to search for, which will default to “all” if we want to return all friends.

The cloud-code for this will be very simple. We will just query the playerFriends collection for friends matching the group requested and return all the friends we find. In this example we only need to return the playerId and displayName, so we will filter the results to only include this data




### Testing

We can test this through the Test-Harness as we’ve done before. If we use the default group “all” you should see all of your friends returned.

For this example, I’ve added a group “family” into the friends requests, so we can also test that this returns specific groups too.


## Player Online Message

The last thing we are going to do is implement a system for notifying players when their friends come online. This is going to require a new ScriptMessage and in this case we will use a system-script instead of creating a new event.
GameSparks already has a script that runs when the player comes online which we can use in this case. You can find this in the System folder in the cloud-code menu of your portal.








### Testing

To test this all we need is to login through the test harness with two players. To show is occurring, you’ll want to login the first player and keep them logged on.
Now, if you login the second player you should see that the first player gets a message through the test-harness if they are on the other player’s friend’s list.

## Additional Options or Features

This tutorial implements a very basic set of features to send and receive friend requests and to get a players list of friends. There is a lot you can do to add additional functionality to this. You can, for example add the players info from the playerList collection to the list of data returned when you get your friends. This would allow you to include things like avatars or other personal information about your friends to your game.
You can also allow friends to use privacy options to check which details they want you to have access to, or how they appear when you search for them.
The important thing is that once you have the friends list, you have access to your friend’s playerId, and you can use this throughout the GameSparks APIs to setup events, matches, challenges or teams to include your friends.
Try it out for yourself and contact customer support or the forums if you need any help in implementing specific features regarding your friends in GameSparks.
