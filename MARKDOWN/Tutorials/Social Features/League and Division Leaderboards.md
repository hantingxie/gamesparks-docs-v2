---
nav_sort: 9
src: /Tutorials/Social Features/League and Division Leaderboards.md
---

# League and Division Leaderboards

This tutorial will demonstrate one way of creating Leaderboards that allocate users' entries based on what league and division they're placed in. Players will also be promoted and demoted depending on how well they did. By using Leaderboards, Events, Cloud Code, Schedulers, Segments, and player scriptData we'll create a system that is both editable and simple.

## Registration and League Placement

When a player in your game registers, their league segment needs to be initialized and they need to be assigned a placement status before they're allocated a league.

First, we ensure that when a player sends a [RegistrationRequest](/API Documentation/Request API/Authentication/RegistrationRequest.md), we input the value *placement* in the *segments* object using a key value pair like this:

```
{
  "@class": ".RegistrationRequest",
  "displayName": "",
  "password": "",
  "segments": {"league":"placement"},
  "userName": ""
}
```
This will help your Cloud Code figure out what to do with a player when they finish a game:
* If the player has a *placement* value set for their league segment, then the Cloud Code will keep track of how many games they played and how well they've done.
* At the end of their placement matches, the Cloud Code will determine the player's league segment based on how well they've done and set their league segment value to Bronze, Silver or Gold.

## Events and Modules

### Modules

We need to create one module.

#### mod_DivisionPlacement

This module will allocate the player in a division in their chosen league. This will fire after the player has been placed in their league, when they're demoted and when they're promoted.

*Cloud Code for mod_DivisionPlacement:*

```
//Load player
var currentPlayer = Spark.loadPlayer(pID);
//While loop condition
var positioned = false;
//Loop counter
var loop = 1;
//Player's league
var league = currentPlayer.getSegmentValue("league");


//While loop will check if divisions have space for this player
while(positioned === false){
   //Load the division based on the loop counter and check if it has space
    var ldrName = "ldr_Global.division.".concat(loop.toString()).concat(".league.").concat(league);
    if(Spark.getLeaderboards().getLeaderboard(ldrName) !== null){
        //Check if there's less than 100 entries (100 players)
        if(Spark.getLeaderboards().getLeaderboard(ldrName).getEntryCount() < 100){
            currentPlayer.setScriptData("division", loop);
            positioned = true;

        }else{  
            //If division is full, look into the next one
            loop = loop + 1;
        }
    } else{
        //If the division doesn't exist, set it as the player's division
        currentPlayer.setScriptData("division", loop);
        positioned = true;
    }
}
```

### Events

We'll need to create and configure three Events for this tutorial.

#### event_InputScore

This Event will be used to update the global Leaderboards and division specific Leaderboards. The player will post their score, league, divison, and the time posted which will help decide which Leaderboard their entry belongs to.

*event_InputScore Attributes:*

| Name  | Shortcode  | Data Type  | Default Val  | Default Aggregation  |
|---|---|---|---|---|
| score  | score  | Number  |   |  Sum |
| league | league  | String  |   | Grouped  |
| division  | division  | Number  |   | Grouped  |
| date  | date  | String  |  ${format(now, "yyyy-MM")} | Grouped  |

#### event_Placement

This event will transfer players from the 'placement' stage to a league and a division.

*event_Placement Attributes:*

| Name  | Shortcode  | Data Type  | Default Val  | Default Aggregation  |
|---|---|---|---|---|
| score  | score  | Number  |   |  Used In Script |

*event_Placement Cloud Code:*

```
//Get input Score value
var inputScore = Spark.getData().score;
//Get player ID
var pID = Spark.getPlayer().getPlayerId();

//Add score to player's placement score
var scriptScore = Spark.getPlayer().getScriptData("placementScore");
 //Check if score is valid
 if (scriptScore !== null){
     var score = scriptScore + inputScore;
     Spark.getPlayer().setScriptData("placementScore", score);
 }
 //If not valid, create it
 else{
     var score = inputScore;
     Spark.getPlayer().setScriptData("placementScore", score);
 }

 //Check how many placement games the player has attempted
 var attempts = Spark.getPlayer().getScriptData("placementAttempts");
 //Check if valid
 if(attempts !== null){
     //If 5 games have been played, check score and place player in the correct league
     if(attempts >= 5){
         if(score >= 3 && score <= 4){
            Spark.getPlayer().setSegmentValue("league", "silver")
         } else if(score >= 5){
            Spark.getPlayer().setSegmentValue("league", "gold")
         } else{
             Spark.getPlayer().setSegmentValue("league", "bronze")
         }
         //Sort division
         require("mod_DivisionPlacement");
     }
     //If player hasn't played 5, increment attempts
     else{
      Spark.getPlayer().setScriptData("placementAttempts", attempts+1);   
     }
     }
//If not valid, create a reference     
else{
    Spark.getPlayer().setScriptData("placementAttempts", 1);
}

```


#### event_EndGame

After every game all players will call this Event. This Event will:
* Determine if they're still in placement or are already in a league and division.
* If players are still in placement stage, the Event will invoke the placement Event.
* If the player is already allocated a league, the Event will invoke *event_InputScore*.

*event_EndGame Attributes:*

| Name  | Shortcode  | Data Type  | Default Val  | Default Aggregation  |
|---|---|---|---|---|
| score  | score  | Number  |   |  Used In Script |

*event_EndGame Cloud Code:*

```
//Load variables
var league = Spark.getPlayer().getSegmentValue("league");
var score = Spark.getData().score;
var date = new Date;


//Check if player has been placed yet
if(league !== "placement"){

    if(Spark.getPlayer().getScriptData("division") === 0){
        require("mod_DivisionPlacement");
    }

    //If player is placed, send a score to be sorted in Leaderboard
    var date = new Date;
    var year = date.getFullYear();
    var month = date.getMonth();
    var request = new SparkRequests.LogEventRequest();

    request.eventKey = "event_InputScore";
    request.score = score;
    request.league = "bronze";
    request.division = 1;
    request.date = year.toString() + "-" + ("0" + (month+1).toString()).slice(-2);

    request.Send();

} else{
    //If player hasn't been placed, update their placement details
    var request = new SparkRequests.LogEventRequest();

    request.eventKey = "event_Placement";
    request.score = score;

    request.Send();

}
```


## Leaderboards

### Global League Leaderboard

This Leaderboard will contain all entries for one league. For example, Bronze entries will be comparable and listed in one Leaderboard regardless of division.

*Global League Leaderboard Fields:*

| Running Total  | Collector  | Filter type | Filter Value | Group  |
|----------------|-------------|--------------|------------|-------|
| Input Score  | event_InputScore.score.all  | *  |   | Sum  |
| Input Score  | event_InputScore.date.all  | *  |   | Partition  |
| Input Score  | event_InputScore.league.all  | =  | bronze  | Maximum  |

Notes:
* The filter value for league would be equal to the league you're creating the leaderboard for. In this example, we use 'bronze' for the Bronze Leaderboard.
* We've also partitioned the Leaderboard by date, so every month a new Leaderboard will created with no entries. Previous Leaderboards and entries can still be retrieved by referencing old dates through the date partition.

### Division Specific Leaderboard

This Leaderboard is configured to keep track of division specific entries so players can compare their record with players in their division.

*Division Specific Leaderboard Fields:*

| Running Total  | Collector  | Filter type | Filter Value | Group  |
|----------------|-------------|--------------|------------|-------|
| Input Score  | event_InputScore.score.all  | *  |   | Sum  |
| Input Score  | event_InputScore.division.all  | *  |   | Partition  |
| Input Score  | event_InputScore.league.all  | *  |   | parition  |

Note:
* Change the Leaderboard's reset frequency if you want to remove entries every day, week, or month to keep your divisions constantly changing.

## Schedule

### Using GS Daily for Promotions and Demotions

At the end of the month we want our players to be demoted and promoted based on how well they did. Once their league is changed they need to be placed in an available league.

The GS Daily script can be found under *Cloud Code>System>Every Day*. The script runs every day. You can use it to create schedule logic. In this example, we check if the day is the first of the month and, if it is, then we run our logic to promote the top 10 and demote the bottom 10 from every league.

*GS Daily Script Cloud Code:*

```
var today = new Date;


if(today.getDate() === 1){

    //Load league Leaderboards
    var bronzeLDR = Spark.getLeaderboards().getLeaderboard("bronze");
    var silverLDR = Spark.getLeaderboards().getLeaderboard("silver");
    var goldLDR = Spark.getLeaderboards().getLeaderboard("gold");;

    //Loads top 10 entries, forget top league because they can't promote
    var bronzeLDR_TOP = bronzeLDR.getEntries(10, 0);
    var silverLDR_TOP = silverLDR.getEntries(10, 0);

    //Loads bottom 10 entries, forget bottom league because they can't demote
    var silverLDR_BOT = silverLDRgetEntries(10, silverLDR.getEntryCount() - 10);
    var goldLDR_BOT = silverLDR.getEntries(10, goldLDR.getEntryCount() - 10);

    //Go through top entries and promote their players
    while(bronzeLDR_TOP.hasNext()){
        var pID = bronzeLDR_TOP.next().getUserId()
        Spark.loadPlayer(pID).setSegmentValue("league", "silver");
    }
    while(silverLDR_TOP.hasNext()){
        var pID = silverLDR_TOP.next().getUserId()
        Spark.loadPlayer(pID).setSegmentValue("league", "gold");
    }

    //Go through bottom entries and demote their players
    while(silverLDR_BOT.hasNext()){
        var pID = silverLDR_BOT.next().getUserId();
        Spark.loadPlayer(pID).setSegmentValue("league", "bronze");

    }
    while(goldLDR_BOT.hasNext()){
        var pID = goldLDR_BOT.next().getUserId();
        Spark.loadPlayer(pID).setSegmentValue("league", "silver");
    }

}
```
