---
nav_sort: 5
src: /Getting Started/Using Cloud Code/Lua Cloud Code.md
---

# Lua Cloud Code

We expect you to have followed the Cloud Code getting started [tutorial](/Getting Started/Using Cloud Code/README.md).

This tutorial will demonstrate saving and loading persistent data against players, specifically the XYZ values from the previous tutorial. You can build an X and Y function instead of an XYZ function by simply omitting the Z variable for each of the steps in the tutorial.

The two main aspects of this tutorial are the *Set* and *Get* functions:
* We'll start with the *Set* function that will take data from the Corona game and send it to the backend.
* We'll then retrieve that data from the backend using the *Get* function.

## Set Function

The *Set* function is composed of three parts:

* Create a [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md).
* Using the *Set_Pos* eventKey for the *Set Position* Event that was configured in the previous [tutorial](/Getting Started/Using Cloud Code/README.md), set the values for the X, Y, and Z variables. Note that in a real example, this function would find the location of your player and send it instead of having hard-set values.
* Send the request and check for errors.

```

--Build request
local requestBuilder = gs.getRequestBuilder()
local saveLocationRequest = requestBuilder.createLogEventRequest()

--Set Values, pay attention to the value POS which is our attribute and the three values which we'll send inside it
saveLocationRequest:setEventKey("Set_Pos")
saveLocationRequest:setEventAttribute("POS",{X=23,Y=23,Z=23})

--Send request and check for errors
saveLocationRequest:send(function(response)
	if response:hasErrors() then
    	for key,value in pairs(response:getErrors()) do print(key,value) end
  end

end)

```

Now the player will have a position variable saved in their scriptData object. You can double-check this by calling an [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md):

1. Through your game and printing out the value of scriptData's 'POS' variable.
2. Through the Test Harness and checking the scriptData object's contents.

## Get Function

As with the *Set* function, we build-up the *Get* function in three parts:
* Create a [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md).
* Set the Event Key value to *Get_Pos*.
* Send the request.

The important aspect of this request is the Response that is received from the backend once it's successfully submitted, processed, and sent back. The process will contain the values we saved because of the Cloud Code we configured in the previous tutorial. Once the response is received by the game it can be broken down and variables can be retrieved from it.

```
--Build Request
local requestBuilder = gs.getRequestBuilder()
local getLocationRequest = requestBuilder.createLogEventRequest()

--Set value for Event Key
getLocationRequest:setEventKey("Get_Pos")

--Send Request
getLocationRequest:send(function(response)
--Process Response
if response:hasErrors() then
    --If errors then print errors
  	for key,value in pairs(response:getErrors()) do print(key,value) end
    --Else extract the POS variable (Type table) and print the contents within it
  else local POS = response:getScriptData().POS
  	for key,value in pairs(POS) do print(key,value) end
  end
  end)

```

These are the basics for data exchange between backend(GameSparks) and frontend(Corona Game) using the GameSparks SDK.

The tutorials in the [next section](/Getting Started/Creating a Leaderboard/README.md) will demonstrate basic Leaderboard creation and use.
