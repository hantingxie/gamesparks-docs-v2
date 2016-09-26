---
nav_sort: 8
src: /Tutorials/Multiplayer/Challenges with Wagers.md
---

# Challenges With Wagers

## Introduction

Having an incentive to win a challenge spices things up, that is why the create challenge request comes built with the ability to wager any of the 6 default currencies but what if that is not enough? This tutorial will teach you how to wager virtual goods through cloud code.  

## The Setup

This tutorial will demonstrate adding extra cloud code to the existing requests and responses that our platform offers to provide extra functionality.  

## Create Challenge Request

When the player creates the challenge, we want to be able to check that the virtual good wager they're placing is valid: that they have enough quantity to wager. In this example we're only ever wagering one virtual good of one type.

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

## Create Challenge Response

The response will save the wager's shortcode for future reference as scriptData linked to the challenge.

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

## Join Challenge Request

When joining a challenge with a virtual good wager a player will be reviewed to see if they're eligible by checking their inventory to see if they have the virtual good. If the player has the virtual good, then they are allowed to join. If the player isn't eligible then we'll force a scriptError to terminate the request.

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

## Challenge Won Message

When a player wins, we want to give them the spoils of their victory. To do this, we will count how many players accepted the challenge and then award the player that amount of virtual goods.

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

## Challenge Lost Message

Losing players will lose their wagered virtual good. We will manually consume these virtual goods using an instance of the ConsumeVirtualGood request.

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
