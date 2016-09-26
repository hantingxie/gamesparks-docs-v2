---
nav_sort: 2
src: /Tutorials/Database Access and Cloud Storage/Searching for Players and Teams.md
---

# Searching for Specific Players and Teams

## Introduction

The platform allows you to search for specific Players and Teams in your game with some very easy to use tools - no matter how big or small the collection.

This tutorial explains several ways you can search for players or teams, using:
* NoSQL Explorer.
* A Player Management screen.
* Cloud Code to find specific entries.  

## Searching with NoSQL Explorer

This powerful tool allows you to search for anything within your game, right down to the specifics of a certain index. For example, you can search for certain players who have exactly 530 ammunition in their inventory or search for players that share the same name - your search possibilities are endless!



<q>**More Information:** For more information about the SQL Explorer, click [here](/Documentation/NoSQL Explorer.md).</q>

### Searching the Player Collection

We'll use the NoSQL explorer to search for a specific player's display name. The display name we'll be looking for will be "Coder".

Here's how we set up the search in the explorer:
* *Collection* - Enter the *Player* collection to limit our search to players only.
* *Query* - Specify what exactly we'll be looking for. In our case, the displayName "Coder".
* *Fields* - Enter the fields for the query in the format: {displayName : "Coder"}.

Once we submit the search (Using enter, or the 'Find' button) the players which have 'Coder' as their display name will be retrieved and all their database data are displayed including scriptData, privateData, externalIDs, external authentication, and many more fields that you may or may not want to see. However, when you search for a certain specific field you can also limit what fields come back from the player database using the format {fieldName: 1} to include fields or {fieldName: 0} to exclude fields. So, for our purpose we're going to limit the search to return displayName and userName fields only:

![](img/TeamsPlayersSearch/1.jpg)

### Searching the Team Collection

Following the search against the Player collection, by changing the collection to 'Team', you can now search for specific teams and view their members, which then allows you to take the member's ID and search for those members:
* If you submit an empty search for your Teams, you will retrieve a list of all your Teams and this will help you see the fields you can query.
* You can search for a specific member by ID to see which team that player belongs to or which teams have earned a certain achievement.

![](img/TeamsPlayersSearch/2.jpg)
   

## Searching with a Player Management Screen

Every game you make in GameSparks comes with our native *Players* management screen, which can be found in the Manage section:
* You can quickly query to retrieve the players you're looking for or display every single player you have in your game's database.
* Unlike the NoSQL Explorer you can view player's details through a graphical interface that you can customize yourself through our dynamic forms builder, for more info, click [here](/Documentation/Manage/Working with Dynamic Forms.md).
* You can also create a Team management screen that functions the same way.
* To ensure that you get exactly what you want you can use rules or group of rules to narrow your search.

![](img/TeamsPlayersSearch/3.jpg)

![](img/TeamsPlayersSearch/4.jpg)


## Searching with Cloud Code

You can also search for Teams and Players in the *Cloud Code*, while your game executes the requests and responses. You can use this powerful capability to allow your users to find each other using events you've set up through Cloud Code.

The following code shows how to use the NoSQL collections to find specific players or teams based on the data we pass in and then using the ID to find references to those players or teams to access the rest of the data:

```    
    //Player search
    //Getting a player based on Query
    var players = Spark.systemCollection("player");

    var playerData = players.findOne({"displayName" : "Coder"}, {_id : 1, displayName:1}); //Find the display name 'Coder' and return the players that have it.

    //Or you can have the player ID saved
    var playerID = "5602c3dce4b07961f34b68c3" //Manually set the ID

    //Finding the player through their ID
    var playerVar = Spark.loadPlayer(playerData.$oid); //or (playerID) //Make a reference for that player through their ID.


    //Team search
    //Getting a Team based on Query
    var Teams = Spark.systemCollection("teams");

    var teamData = Teams.findOne({"teamName" : "BlueGang"}, {_id : 1, teamName:1}); //Find the team name 'BlueGang' and return the teams that have it

    //Or you can have the player ID saved
    var teamID = "GameSparks Team" //manually set the ID

    //Finding the player through their ID
    var teamVar = Spark.getTeams().getTeam(teamData.$oid); // or (teamID) //Make a reference for that team through the ID

```
