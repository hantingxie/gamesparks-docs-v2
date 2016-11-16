---
nav_sort: 4
src: /Getting Started/Creating an Achievement/Lua Achievements.md
---

# Lua Achievements

This tutorial demonstrates how to reward a player with an Achievement configured in the [previous tutorial](/Getting Started/Creating an Achievement/README.md) and how to notify the player that they've received it.

## Setting up your Listener

We'll be listening in for the *onAchievementEarned* message, which will trigger when our player earns an Achievement:

```
local function onAchievementMessage(AchievementEarnedMessage)
print("You earned the " .. AchievementEarnedMessage:getAchievementName())
end

```

The message is received and the Achievement name is retrieved then used in a print function.

Bind the function you just made to be invoked every time an *AchievementEarned* Message is received by the game.

```
gs.getMessageHandler().setAchievementEarnedMessageHandler(onAchievementMessage)

```

## Awarding the Achievement to the Player

We'll be using the Event we configured in the [previous tutorial](/Getting Started/Creating an Achievement/README.md) to award the player the *Cloud Achievement*

```

--Build Request
local requestBuilder = gs.getRequestBuilder()
local awardAchievementRequest = requestBuilder.createLogEventRequest()

--Set Value of Event Key
awardAchievementRequest:setEventKey("Award_Achievement")

--Send
awardAchievementRequest:send()

```
Once sent, the player will receive a message congratulating them on their new Achievement if it's the first time they've earned it.

In the [next tutorial](/Getting Started/Creating a Virtual Good/README.md) we'll demonstrate Virtual Goods and how to retrieve a player's record and display their Achievements and Virtual Goods.  
