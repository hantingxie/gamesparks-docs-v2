---
nav_sort: 11
src: /Tutorials/Real-Time Services/Corona Real-Time Guide.md
---

# Corona Real-Time Guide

This is a guide for getting your Corona project set up for GameSpark's real-time services.

<q>**Read First!** Please ensure you have followed our general guide on [real-time services](/Tutorials/Real-Time Services/Understanding GameSparks Real-Time.md) before you attempt to apply it for Corona and to learn how our real-time service works and what you should expect from it.</q>

## Creating the GameSession File

*1.* Create a *GameSession.lua* file. This file will save the default settings for the session and how it should react to incoming packets and events.

*2.* Copy the following [class](https://bitbucket.org/gamesparks/gamesparks-corona/src/40e3b0c3f3a2d6ac05ac3fa242f4c877d008ab43/lua/GameSession.lua?at=default&fileviewer=file-view-default) and paste it in your GameSession file.

## Setup

Somewhere in your game logic have the following setup. For this example we have it in main.lua.

*1.* Require the necessary libraries:

```
local gs = require("plugin.gamesparks")
local gsrt = gs.getRealTimeServices()
local GameSession = require("GameSession")
```

*2.* Declare the session for future use:

```
local mySession = nil
```

*3.* Create a function to send a matchmaking request:

```
local function sendMatchmakingRequest()
  local requestBuilder = gs.getRequestBuilder()
  local matchmakingRequest = requestBuilder.createMatchmakingRequest()

  matchmakingRequest:setSkill(1)
  matchmakingRequest:setMatchShortCode("Your RT Match ShortCode here")
  matchmakingRequest:send(function(matchmakingResponse)
  --If there's any errors, print them out
    if matchmakingResponse:hasErrors() then
        for key,value in pairs(matchmakingResponse:getErrors()) do
          print(key,value)
        end
      else
        print("Match OK...")
      end
  end)
end
```
*4.* Add a listener for both Match Found and Match Not Found messages. We'll be adding more logic to the Match Found Message regarding packet/data delivery later down the tutorial:

```
gs.getMessageHandler().setMatchFoundMessageHandler(function(message)
--When match is found, instantiate the real-time session
mySession = GameSession.new(message:getAccessToken(), message:getHost(), message:getPort())
end)


gs.getMessageHandler().setMatchNotFoundMessageHandler(function(message)
 print("MATCH NOT FOUND")
-- Send matchmaking request again if failed to find a match
 sendMatchmakingRequest()
end)
```

*5.* In your update function add:

```
-- If session instance is not null
local function myUpdate()
-- If session is instantiated
  if mySession then
  --Update RT Session
    mySession.session:update()

  end
end
```

## Sending Packets

To send packets:

*1.* Create a RTData object:

```
local data = gs.getRTData().new()
```

*2.* If you wish to send data with your packet then populate your RTData object with variables. Starting first with the index of the variable and then the value:

```
--Set Number
data:setLong(1, varLong)
--Set Vector
data:setRTVector(2, varVector)
--Set Float
data:setFloat(33, varFloat)
--Set Double
data:setDouble(56, varDouble)
--Set String
data:setString(78, varString)
--set nested data object
data:setData(90, varData)

```
*3.* Send the Data in a packet through the session's send function. Give the packet an OPCode, the RTData object, the intent, and the recipients (If the recipients are not specified, the packet will be sent to all active players) and send it:

```
  mySession.session:sendRTData(1, gsrt.deliveryIntent.RELIABLE, data, {})

```
## Receiving Packets

In your Match Found listener, add the logic to change your onPacket callback functionality to suit the packets you're sending:

```
-- Message found handler from above
gs.getMessageHandler().setMatchFoundMessageHandler(function(message)
mySession = GameSession.new(message:getAccessToken(), message:getHost(), message:getPort())

-- Set the new callback depending on the packets you wish to recieve
mySession.onPacketCB = function(packet)
-- Choose what to do with a packet depending on its opCode
if packet.opCode == 1 then
-- Use packet.data to access the data in your packet and reference the type and index position of the variable
	print("DATA IS " .. packet.data:getLong(1))
end

end

end)
```
