---
nav_sort: 8
src: /Tutorials/Multiplayer/Challenges with Wagers.md
---

# Challenges With Wagers

## Introduction

Having an incentive to win a Challenge spices things up and that's why the [CreateChallengeRequest](/API Documentation/Request API/Multiplayer/CreateChallengeRequest.md) comes built with the ability to wager any of the 6 default currencies. But what if that is not enough?

This tutorial shows you how to wager Virtual Goods through Cloud Code.

## The Setup

More generally, this tutorial demonstrates how to add extra Cloud Code to the existing requests and responses that our platform offers to provide extra functionality.  

### Create Challenge Request

When the player creates the Challenge using a *CreateChallengeRequest*, we want to be able to check that the Virtual Good wager they're placing is valid - that is, check the player has enough quantity to wager. In this example we're only ever wagering one Virtual Good of one type:

```    
  //Check if we have scriptData
  if(Spark.getData().scriptData){

  //Set value of virtualGoodWager
  var virtualGoodWager = Spark.data.scriptData.virtualGoodWager;
  //Load up the player's inventory
  var Vgoods = Spark.getPlayer().getVirtualGoods();


  //Does player have enough?
  if(Spark.getPlayer().hasVGood(virtualGoodWager) > 0)
        {
            //if yes, then setScript code for the response to use
            Spark.setScriptData("virtualGoodWager", virtualGoodWager);
        }
        else
        {
            //If no, then set error script to terminate request
            Spark.setScriptError("Error", "Don't have the right virtual good to wager");
        }
    }

```    

### Create Challenge Response

The *CreateChallengeResponse* will save the wager's *Short Code* for future reference as *scriptData* linked to the Challenge:

```
    if(Spark.getData().scriptData.virtualGoodWager){

        //Get the scriptdata from the request
        var virtualGoodWager = Spark.data.scriptData.virtualGoodWager;
        //Load the challenge
        var currentChallenge = Spark.getChallenge(Spark.getData().challengeInstanceId);
        //Set scriptData
        currentChallenge.setScriptData("virtualGoodWager", virtualGoodWager);   
    }

```

### Join Challenge Request

When joining a Challenge with a Virtual Good wager, a player will be reviewed to see if they're eligible by checking their inventory to see if they have the virtual good. If the player has the Virtual Good, then they are allowed to join. If the player isn't eligible to join, then we'll force a *scriptError* to terminate the request:

```
    //Save instance ID
    var challengeInstanceIdVar = Spark.getData().challengeInstanceId;

    //Load up challenge
    var currentChallenge = Spark.getChallenge(challengeInstanceIdVar);

    var virtualGoodWager = currentChallenge.getScriptData("virtualGoodWager");
    //if challenge have scriptData
    if(virtualGoodWager){

        //Does player have enough quantity?
        if(Spark.getPlayer().hasVGood(virtualGoodWager) > 0) {
            //if yes, carry on
        }
        else {
            //if no, terminate
            Spark.setScriptError("Error", "Don't have enough to wager inorder partake in challenge")
        }

    }

```

### Challenge Won Message

When a player wins, we want to give them the spoils of their victory. To do this, we'll count how many players accepted the Challenge and then award the player that amount of Virtual Goods:

```

    //Check for scriptData
    if(Spark.getData().challenge.scriptData.virtualGoodWager){

        //Save shortcode
        var itemWager = Spark.getData().challenge.scriptData.virtualGoodWager;

        //Save number of players
        var playerCount = Spark.getChallenge(Spark.getData().challenge.challengeId).getAcceptedPlayerIds().length;

        //Award the winner the wager of the losers
        Spark.getPlayer().addVGood(itemWager, playerCount);
    }

```

### Challenge Lost Message

Losing players will lose their wagered Virtual Good. We'll manually consume these Virtual Goods using an instance of the [ConsumeVirtualGoodRequest](/API Documentation/Request API/Store/ConsumeVirtualGoodRequest.md):

```
    //Does the challange have any scriptData
    if(Spark.getData().challenge.scriptData)
    {
        //The shortcode for the virtual good
        var itemWager = Spark.getData().challenge.scriptData.virtualGoodWager;

        //New instant of consume request
        var consumeRequest = new SparkRequests.ConsumeVirtualGoodRequest();

        //Pass in parameters
        consumeRequest.quantity = 1;
        consumeRequest.shortCode = itemWager;

        //Reference the response
        consumeResponse = consumeRequest.Send();

        //Set response as scriptData with this message
        Spark.setScriptData("Response", consumeResponse);
    }

```
