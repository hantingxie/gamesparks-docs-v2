---
nav_sort: 1
src: /Tutorials/Multiplayer/Hearthstone Example/Initialization and Ranking.md
---

# Initialization and Ranking

## First, the Cards

For a game like this to work we need a way to store the game's cards somewhere where it will be easy to access, manage, and edit them. For this, we'll use the platform's mongo database.

First, head over to the NoSQL tab. Click the 'Create' tab and create three runtime collections. Call these collections *commonCards*, *rareCards*, and  *legendaryCards*.

Once those collections are made, its time to populate them. Each card will be it's own document, and the reasons will be obvious further down the tutorial. To populate your collections, click the 'Insert' tab. And insert a document, for example: {"cardName": "Warrior", "tier": "commonCards", "attack": 1, "health": 2, "spawnCost": 1, "effect": "Charge"} which will result in our document looking like this:

```

{
 "_id": {
  "$oid": "56cf0e2ee4b07371e6a6ddc7"
 },
 "cardName": "Warrior",
 "tier": "commonCards",
 "attack": 1,
 "health": 2,
 "spawnCost": 1,
 "effect": "Charge"
}

```

The card consists of an Id which is automatically generated, you don't have to create it. A cardName which represents the type of card, the teir which will help us find the collection a card belongs to, the base attack, base health, spawn cost and the effect of the card if any. Continue to fill the collections with cards. Our tutorial has 3 commonCards, 3 rareCards and 1 legendaryCards.

## Player Initilisation

We'll need to initialize our players once they're registered by giving them a basic deck and a starting rank. To do this, we need to add scriptData to the player once they register. Head over to the cloud code section under the configurator tab on the platform. Once there, navigate to the responses tab, expand it and look for the RegistrationResponse. We edited our RestrationReponse to look like this:

```

//Set rank to the lowest and declare stars
Spark.getPlayer().setScriptData("rank", 25);
Spark.getPlayer().setScriptData("stars", 0);

//Load up the rare cards collection
var cardCollection = Spark.runtimeCollection("rareCards");

//Declare length of collection
var length = cardCollection.count() - 1;
//Declare a random number between start and length of collection
var randNum = Math.floor(Math.random() * (length - 0 + 1));
//Retrieve a random document which represents a card
var doc = cardCollection.find().limit(-1).skip(randNum).next();

//Save that card on the player's deck including default common cards
Spark.getPlayer().setPrivateData("deck", [{"name":doc.cardName,"tier":doc.tier}, {"name":"Mage","tier":"commonCards" }, {"name":"Archer","tier":"commonCards" }, {"name":"Warrior","tier":"commonCards" }]);

//Output which card was recieved
Spark.setScriptData("Your starter rare card", doc.cardName);

```

Our registration response will set the player's rank to 25 with no stars. The response will also construct the player's deck by giving them a random rare card and all the common cards(Done manually). The deck will also be saved in privateData instead of scriptData because once the player's deck gets bigger and if later you give your players a chance to make more decks the player's details will get clogged, so we'll leave the deck in privateData and retrieve it when we want to using an event.

## Ranking

When a player loses or wins in a ranked match their rank and stars will be affected. So it's only logical to place this logic in the ChallengeWon and ChallengeLost messages which can be found under the UserMessages tab in the cloud code section. Within these messages, we'll be calling a module which will process the ranking after the result of the challenge.

ChallengeWonMessage:

```

//If it's a ranked match, process rank
if(Spark.getData().challenge.shortCode === "chalRanked")
{
    //This player was victorious so declare the outcome to 'Victory'
    var outcome = "victory";

    //Depending on the outcome variable the 'processRank' module will either increase rank or decrease player rank
    require("processRank");
}

```

ChallengeLostMessage:

```

//If it's a ranked match, process rank
if(Spark.getData().challenge.shortCode === "chalRanked")
{
    //This player lost so declare the outcome to 'loss'
    var outcome = "loss";

    //Depending on the outcome variable the 'processRank' module will either increase rank or decrease player rank
    require("processRank");
}

```

The processRank module level the player up or down depending on the outcome of the challenge.

The processRank module:

```
//Retrieve the number of stars the player earned
var currentStars = Spark.getPlayer().getScriptData("stars");
//Retrieve current rank
var currentRank = Spark.getPlayer().getScriptData("rank");


if(outcome === "victory"){

    //Because the player just won, add a star
    currentStars++;
    //Save the number of stars the player has
    Spark.getPlayer().setScriptData("stars", currentStars);

    //Check for rank range
    if(currentRank >= 25 && currentRank <= 21 ){

        //Check for number of stars and if they qualify a levelup
        if (currentStars >= 2){
            //If number is met, level up by decending down towards rank 1
            Spark.getPlayer().setScriptData("rank", currentRank - 1);
            //Reset and save the number of current stars
            Spark.getPlayer().setScriptData("stars", 0);
        }

    }
    else if(currentRank >= 20 && currentRank <= 16 ){
        //Check for number of stars and if they qualify a levelup
        if (currentStars >= 3){
            //If number is met, level up by decending down towards rank 1
            Spark.getPlayer().setScriptData("rank", currentRank - 1);
            //Reset and save the number of current stars
            Spark.getPlayer().setScriptData("stars", 0);
        }
    }
    else if(currentRank >= 15 && currentRank <= 11 ){
        //Check for number of stars and if they qualify a levelup
        if (currentStars >= 4){
            //If number is met, level up by decending down towards rank 1
            Spark.getPlayer().setScriptData("rank", currentRank - 1);
            //Reset and save the number of current stars
            Spark.getPlayer().setScriptData("stars", 0);
        }
    }
    else{

        //Don't do anything if player is rank 1 because they can't advance anymore
        if(currentRank > 1)
        {
            //Check for number of stars and if they qualify a levelup         
            if (currentStars >= 5){
                //If number is met, level up by decending down towards rank 1
                Spark.getPlayer().setScriptData("rank", currentRank - 1);
                //Reset and save the number of current stars
                Spark.getPlayer().setScriptData("stars", 0);
            }
        }
    }
}

else{

    //Does the player have stars?
    if(currentStars > 0){

    //Because the player just lost, remove a star
    currentStars--;
    //Save the number of stars the player has
    Spark.getPlayer().setScriptData("stars", currentStars);

    }

    //Check if player rank is less than 25 because that's the lowest level
    if(currentRank < 25){
        //If player has 0 stars
        if(currentStars < 1){
            //Decrease level by 1
            Spark.getPlayer().setScriptData("rank", currentRank + 1);

            if(currentRank >= 1 && currentRank <= 9){
                Spark.getPlayer().setScriptData("stars", 5);
            }
            if(currentRank >= 10 && currentRank <= 14 ){
                Spark.getPlayer().setScriptData("stars", 4);
            }
            if(currentRank >= 15 && currentRank <= 19){
                Spark.getPlayer().setScriptData("stars", 3);
            }
            if(currentRank >= 20 && currentRank <= 24){
                Spark.getPlayer().setScriptData("stars", 2);
            }

        }

    }
}

```

## ChallengeTurnTaken Message

This is a brilliant message to place a check for player's health and act upon it because it's called after every challenge event is executed. We will have three checks, whether the challenger's health is 0 or lower and the challenged player's health is over 0; whether the challenged player's health is 0 or lower and the challenger's health is over 0; and finally if both player's healths are equal to or lower than 0. Each condition will trigger a different response, either the challenger winning, the challenged winning or both drawing.

```
//Load challenge
var chal = Spark.getChallenge(Spark.getData().challenge.challengeId);

//load playerStats
var playerStats = Spark.getScriptData("playerStats");

//If challenger reaches 0 or lower health while challenged has more than 0 health, challenged wins
if(playerStats[chal.getChallengerId()].currentHealth <= 0 && playerStats[chal.getChallengedPlayerIds()[0]].currentHealth > 0){
    chal.winChallenge(Spark.loadPlayer(chal.getChallengedPlayerIds()[0]));
}
//If challenged reaches 0 or lower health whole challenger has more than 0 health, challenger wins
if(playerStats[chal.getChallengedPlayerIds()[0]].currentHealth <= 0 && playerStats[chal.getChallengerId()].currentHealth > 0){
    chal.winChallenge(chal.getChallengerId());
}
//If both players reach zero or lower health, a draw is in order
if(playerStats[chal.getChallengedPlayerIds()[0]].currentHealth <= 0 && playerStats[chal.getChallengerId()].currentHealth <= 0){
    chal.drawChallenge();
}

```

And that's it for initilisation, your game is ready for the matchmaking.
