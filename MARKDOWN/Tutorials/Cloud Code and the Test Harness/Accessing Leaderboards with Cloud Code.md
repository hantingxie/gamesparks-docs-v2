---
nav_sort: 4
src: /Tutorials/Cloud Code and the Test Harness/Accessing Leaderboards with Cloud Code.md
---

# How to Access Leaderboards via Cloud Code

There are many scenarios where you might want to access Leaderboard data. For example, you might want to:
* Determine the position of given player within a Leaderboard.
* Get the id of a player who is at a given position on the Leaderboard.

You can implement these two features using the Cloud Code [SparkRequests](/Tutorials/Cloud code and the Test Harness/Using SparkRequests API to Send Requests in Cloud Code.md) API. This API allows requests to be sent either as the current player or as any other player within your game.

To find the rank of a given player, you can use a [LeaderboardDataRequest](/API Documentation/Request API/Leaderboards/LeaderboardDataRequest.md), which will return the data associated with the player:

```    
    var request = new SparkRequests.LeaderboardDataRequest();
    request.entryCount = 1;
    request.leaderboardShortCode = "leaderboardSC";

    var response = request.Send();

```
Now you'll have the GameSparks response stored in your response variable as a JSON object.
