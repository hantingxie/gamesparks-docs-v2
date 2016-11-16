---
nav_sort: 4
src: /Getting Started/Creating a Leaderboard/Lua Leaderboards.md
---

# Lua Leaderboards

This tutorial will demonstrate sending a score from your game, creating a Leaderboard entry from it, and setting up a message interceptor/listener to process specific messages sent to the currently authenticated player.

## Setting Up your Listener

We'll be listening in for the newHighScore message which will trigger when our player submits a high score for the Leaderboard.

First we'll create the function which will handle the message:

```
local function onNewHighScoreMessage(newHighScoreMessage)
print("You earned the highscore in the Leaderboard " .. newHighScoreMessage:getLeaderboardName())
end

```
The message is received and the Leaderboard name is retrieved then used in a print function.

Bind the function you just made to be invoked everytime a newHighScore message is received by the game.

```
gs.getMessageHandler().setNewHighScoreMessageHandler(onNewHighScoreMessage)

```

## Sending your Player's Score

We'll be using the Event we configured in the previous [tutorial](/Getting Started/Creating a Leaderboard/README.md) to send our player's score to the backend which will process the score and create a Leaderboard entry from it.

```
local function postScore()
--Build Request
local requestBuilder = gs.getRequestBuilder()
local postScoreRequest = requestBuilder.createLogEventRequest()

--Set values, pay attention to the SCORER variable which is used to send the score to the leaderboard
postScoreRequest:setEventKey("Leaderboard_Scorer")
postScoreRequest:setEventAttribute("SCORER", 1201)

--Send Request
postScoreRequest:send()

end
```

Once the score has been sent and the highscore has been beaten, your player will receive a message congratulating them on beating the highscore.

To look at the results of the Leaderboard, create a [LeaderboardDataRequest](/API Documentation/Request API/Leaderboards/LeaderboardDataRequest.md) and set the value for entries you want back and the Short Code for the Leaderboard you wish to view:


```
local function printEntries()
--Build Request
local requestBuilder = gs.getRequestBuilder()
local getEntryRequest = requestBuilder.createLeaderboardDataRequest()

--Set values
getEntryRequest:setLeaderboardShortCode("HIGH_SCORE")
getEntryRequest:setEntryCount(50)

--Process response by printing the entries in the format Username, Score then Rank using a for loop. Use getAttribute() for your custom values
getEntryRequest:send(function(response)
	 local entries = response:getData()
	 for i, entry in pairs(entries) do
	 	print(entry:getUserName() , entry:getAttribute("SCORER") , entry:getRank())
	 end
end)

end

```

These are the basics to message handlers/listeners and Leaderboard score submission and entry printing. There are a few more requests that deal with Leaderboards, please check our [API documentation](/API Documentation/README.md) for more information.
