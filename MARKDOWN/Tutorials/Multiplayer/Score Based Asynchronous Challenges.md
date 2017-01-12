---
nav_sort: 10
src: /Tutorials/Multiplayer/Score Based Asynchronous Challenges.md
---

# Score Based Asynchronous Challenges

By default, GameSparks Challenges require both players to accept the Challenge before posting their scores. While this is ideal for some games, it's not the best for spontaneously challenging a friend to a game and saying: "Hey! Bet you can't beat this!"

Asynchronous Challenges are turn-based multiplayer gameplay between two or more players that can check in and play their turn when it's convenient. Similar to play-by-mail games and, more electronically, play-by-email.

## Asynchronous Challenge Flow

The flow of an Asynchronous Challenge looks like:

1\. Player 1 gets an awesome score, decides to challenge another user to beat it.

2\. Player 1 picks who to challenge and sends a [CreateChallengeRequest](/API Documentation/Request API/Multiplayer/CreateChallengeRequest.md) to the user of their choice (Player 2).

3\. Player 1 receives a successful *CreateChallengeResponse*, takes the *ChallengeInstanceId* and sends a [LogChallengeEventRequest](/API Documentation/Request API/Multiplayer/LogChallengeEventRequest.md) to save their score in that Challenge Instances ScriptData.

<q>**Note:** In your code this should all happen very quickly.</q>

4\. Player 2 receives a message that Player 1 has challenged them to beat their score.

5\. Player 2 sends a [GetChallengeRequest](/API Documentation/Request API/Multiplayer/GetChallengeRequest.md) to retrieve the latest details of the challenge (including Player 1's score in the Script Data).

6\. Player 2 sends an [AcceptChallengeRequest](/API Documentation/Request API/Multiplayer/AcceptChallengeRequest.md) and on a successful *AcceptChallengeResponse* the game loads the appropriate level.

7\. Player 2 gets a score and sends a *LogChallengeEventRequest* with their score and the Cloud Code script will decide the winner.

8\. Both Player 1 and Player 2 receive a message declaring who won and who lost.

## Setting Up Asynchronous Challenges

*1.* Create a *SetScoreOnChallenge* Event. It should look like:

![](img/ScoreBasedAsynchChallenges/1.png)

* We'll take the *challengeInstanceId* so we know which *challengeInstance* we want to save the score in.
* We'll also take the score we want to save.

*2.* Click to *Save and Close* the new Event.

*4.* Create the *SetScoreAndCalculateOutcome* Event, which should look like:

![](img/ScoreBasedAsynchChallenges/2.png)

* This one doesn't take a *challengeInstanceId* attribute because this will only ever be called with a *LogChallengeEvent*, which already includes the *challengeInstanceId*.
* We don't use *LogChallengeEvent* for the previous Event because it has logic associated with progressing the Challenge.

*5.* Click to *Save and Close* the new Event.

*6.* Create the Challenge:

![](img/ScoreBasedAsynchChallenges/3.png)

<q>**Important!** Two things to take note of here: First, **Turn / Attempt Consumers** which has been set to our *SetScoreAndCalculateOutcome* Event; Second, **Leaderboard** which has been set to *Scripted Outcome* and this means we can run custom logic to determine the victor.</q>

*7.* Click to *Save and Close* the Challenge.

*8.* Add in your Cloud Code:

First, navigate to *Configurator > Cloud Code > Events > SetScoreOnChallenge* and add in the following:

```
    //Load our challenge with the challengeId we passed
    var challenge = Spark.getChallenge(Spark.getData().challengeInstanceId);
     
    //We get the score attribute passed from our game
    var player1Score = Spark.getData().score;
     
    //Store the turns in our challenge's scriptData
    challenge.setScriptData("player1Score", player1Score);

```

Second, navigate to *Configurator > Cloud Code > Challenge Events > SetScoreAndCalculateOutcome* and add in the following:

```
    //Load our challenge
    var challenge = Spark.getChallenge(Spark.getData().challengeInstanceId);
     
    //We get the score attribute and save it to the scriptData
    var player2Score = Spark.getData().score;
    challenge.setScriptData("player2Score", player2Score);
     
    //Player 1 will be our challenger
    var player1 = Spark.loadPlayer(challenge.getChallengerId());
     
    var player1Score = challenge.getScriptData("player1Score")
     
    //Player 2 is the player who triggered this event
    var player2 = Spark.getPlayer();
    //We could also load players from challenge.getChallengedPlayerIds()[] or challenge.getAcceptedPlayerIds()[]
     
     
    //Call our play function
    play();
     
    function play()
    {
         
        if(player1Score > player2Score){
             
            //challenge.setScriptData("winner", player1);
            challenge.winChallenge(player1);
        }
         
        if(player2Score > player1Score){
             
            //challenge.setScriptData("winner", player2);
            challenge.winChallenge(player2);
        }
    }

```

<q>**Ready to Test!** With that done we are ready to test.</q>

*5.* Head on over to the [Test Harness](/Documentation/Test Harness/README.md) and follow along:

Player 1 gets an awesome score and picks a friend to challenge:

```    
    {
     "@class": ".CreateChallengeRequest",
     "accessType": "PRIVATE",
     "challengeShortCode": "asyncChallenge",
     "endTime": "2015-02-19T00:00Z",
     "usersToChallenge": "54d0b761e4b021c187558337"
    }
     
    {
     "@class": ".CreateChallengeResponse",
     "challengeInstanceId": "54d0d867e4b021c187559b13",
     
    }

```

In our game, on a successful *CreateChallengeResponse* we'll take the newly created *challengeInstanceId* and immediately send a *LogEventRequest* to post our score:

```    
    {
     "@class": ".LogEventRequest",
     "eventKey": "SetScoreOnChallenge",
     "challengeInstanceId": "54d0d867e4b021c187559b13",
     "score": "356"
    }
     
    {
     "@class": ".LogEventResponse",
     
    }

```

Player 1 has now challenged their friend and set their score in the ScriptData of the Challenge, they can go back to playing their game.

Player 2 will receive a message (or push notification!) alerting them that Player 1 has gotten a crazy high score on your game, it will look something like this:

```    
{
 "@class": ".ChallengeIssuedMessage",
 "messageId": "54d0d867e4b021c187559b14",
 "notification": true,
 "summary": ".ChallengeIssuedMessage",
 "who": "oisin",
 "challenge": {
  "challengeId": "54d0d867e4b021c187559b13",
  "state": "ISSUED",
  "scriptData": {},
  "shortCode": "asyncChallenge",
  "startDate": null,
  "accepted": [
   {
    "name": "oisin",
    "id": "54d0b768e4b021c187558356"
   }
  ],
  "challenged": [
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenger": {
   "name": "oisin",
   "id": "54d0b768e4b021c187558356"
  },
  "expiryDate": null,
  "endDate": "2015-02-19T00:00Z",
  "challengeName": "Asynchronous Challenge"
 },
 "playerId": "54d0b761e4b021c187558337"
}

```

You'll notice the *scriptData* is empty, that's because the message was sent before we logged our score to the Challenge. To overcome this, we can use *GetChallengeRequest* which will reflect the updated Challenge:

```
{
 "@class": ".GetChallengeRequest",
 "challengeInstanceId": "54d0d867e4b021c187559b13"
}

```
```
{
 "@class": ".GetChallengeResponse",
 "challenge": {
  "challengeId": "54d0d867e4b021c187559b13",
  "state": "ISSUED",
  "scriptData": {
   "player1Score": "356"
  },
  "shortCode": "asyncChallenge",
  "startDate": null,
  "accepted": [
   {
    "name": "oisin",
    "id": "54d0b768e4b021c187558356"
   }
  ],
  "challenged": [
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenger": {
   "name": "oisin",
   "id": "54d0b768e4b021c187558356"
  },
  "expiryDate": null,
  "endDate": "2015-02-19T00:00Z",
  "challengeName": "Asynchronous Challenge"
 },

}

```
Now that we have the Challenge details, we can display the relevant details to Player 2. Next, we have Player 2 send an *AcceptChallengeRequest* and launch the level they will be playing:

```
{
 "@class": ".AcceptChallengeRequest",
 "challengeInstanceId": "54d0d867e4b021c187559b13"
}

```

Both players will receive a message that Player 2 has accepted the game:

```
{
 "@class": ".ChallengeStartedMessage",
 "messageId": "54d0db88e4b021c187559cab",
 "notification": true,
 "summary": ".ChallengeStartedMessage",
 "challenge": {
  "challengeId": "54d0d867e4b021c187559b13",
  "state": "RUNNING",
  "scriptData": {
   "player1Score": "356"
  },
  "shortCode": "asyncChallenge",
  "startDate": "2015-02-03T14:30Z",
  "accepted": [
   {
    "name": "oisin",
    "id": "54d0b768e4b021c187558356"
   },
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenged": [
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenger": {
   "name": "oisin",
   "id": "54d0b768e4b021c187558356"
  },
  "expiryDate": null,
  "endDate": "2015-02-19T00:00Z",
  "challengeName": "Asynchronous Challenge"
 },
 "playerId": "54d0b761e4b021c187558337"
}

```

Player 2 gets a pretty good score, but not good enough to beat Player 1, so we now call our *LogChallengeEventRequest*:
```
{
 "@class": ".LogChallengeEventRequest",
 "eventKey": "SetScoreAndCalculateOutcome",
 "challengeInstanceId": "54d0d867e4b021c187559b13",
 "score": "212"
}

```

Both Players now get either a *ChallengeWonMessage* or a *ChallengeLostMessage*:

Player 2 receives:
```
{
 "@class": ".ChallengeLostMessage",
 "messageId": "54d0dc43e4b021c187559ce0",
 "notification": true,
 "summary": ".ChallengeLostMessage",
 "winnerName": "oisin",
 "challenge": {
  "challengeId": "54d0d867e4b021c187559b13",
  "state": "COMPLETE",
  "scriptData": {
   "player1Score": "356",
   "player2Score": "212"
  },
  "shortCode": "asyncChallenge",
  "startDate": "2015-02-03T14:30Z",
  "accepted": [
   {
    "name": "oisin",
    "id": "54d0b768e4b021c187558356"
   },
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"


}
  ],
  "challenged": [
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenger": {
   "name": "oisin",
   "id": "54d0b768e4b021c187558356"
  },
  "expiryDate": null,
  "endDate": "2015-02-19T00:00Z",
  "challengeName": "Asynchronous Challenge"
 },
 "playerId": "54d0b761e4b021c187558337"
}

```

Player 1 receives:

```
{
 "@class": ".ChallengeWonMessage",
 "messageId": "54d0dc43e4b021c187559cdd",
 "notification": true,
 "summary": ".ChallengeWonMessage",
 "currency1Won": 0,
 "currency2Won": 0,
 "currency3Won": 0,
 "currency4Won": 0,
 "currency5Won": 0,
 "currency6Won": 0,
 "challenge": {
  "challengeId": "54d0d867e4b021c187559b13",
  "state": "COMPLETE",
  "scriptData": {
   "player1Score": "356",
   "player2Score": "212"
  },
  "shortCode": "asyncChallenge",
  "startDate": "2015-02-03T14:30Z",
  "accepted": [
   {
    "name": "oisin",
    "id": "54d0b768e4b021c187558356"
   },
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenged": [
   {
    "name": "shane",
    "id": "54d0b761e4b021c187558337"
   }
  ],
  "challenger": {
   "name": "oisin",
   "id": "54d0b768e4b021c187558356"
  },
  "expiryDate": null,
  "endDate": "2015-02-19T00:00Z",
  "challengeName": "Asynchronous Challenge"
 },
 "playerId": "54d0b768e4b021c187558356"
}

```
