---
nav_sort: 7
src: /Tutorials/Multiplayer/Match Based Challenges.md
---

# Match Based Challenges

## Introduction

Once you match players together you will have reference to other player's PlayerIDs and account variables to use in Cloud code and use of useful platform features. One of these features is challenging matched players to a private challenge. This combination of Matchmaking and Challenge initiation ensures players are matched up in accordance to a set of rules revolving around skill level.

## Connecting the Match to the Challenge

To invite the matched up players to a challenge:

  * Call the MatchDetail request to access the 'Opponents' Player array and access the ID string variable.
  * Call the CreateChallenge request. For the AccessType use PRIVATE because you'll want to invite players from the Match and not allow any other players in.
  * For the string array 'Users to Challenge' use the IDs you accessed through the MatchDetail response.
  * Configure the rest of the challenge and send the CreateChallenge request.
  * The players invited should receive messages notifying them they've been invited. (Use listeners to capture these).
  * Once all player's have replied by either accepting or declining the challenge is then started.

You can test this using the Test Harness by opening multiple tabs and authenticating multiple players. Match these players up and then use the MatchDetails request and CreateChallenge request to simulate calling them from an SDK.


### Example Request

```
    {
     "@class": ".CreateChallengeRequest",
     "accessType": "PRIVATE",
     "autoStartJoinedChallengeOnMaxPlayers": false,
     "challengeMessage": "Welcome to this Challenge",
     "challengeShortCode": "Trigger_Chal",
     "endTime": "2015-12-30T12:00Z",
     "expiryTime": "2015-12-30T12:00Z",
     "usersToChallenge": [
     "563b4243e4b0f85acff00a69","563b4235e4b0f85acff00a22",
    "563b4235e4b0f85acff00a22"]
    }

```
