---
nav_sort: 5
src: /Getting Started/Creating a Game/Corona Setup.md
---

# Corona Setup

## Integrating with GameSparks

Integrating Corona with GameSparks is straightforward. There are 3 steps:

*1.* Download the latest SDK from the GameSparks Bitbucket repository.

* **Example Corona Setup** code can be downloaded [here](http://repo.gamesparks.net/docs/tutorial-assets/XYZXYZ)

*2.* Copy the folder 'GameSparks' in the example project and place it in your own project.

*3.* Open the Build.settings of your project and add the following:

```
  plugins =
    {
        ["plugin.bit"] =
        {
            publisherId = "com.coronalabs",
        },
        ["plugin.openssl"] =
        {
            publisherId = "com.coronalabs",
        },
    },

```

Now you'll have access to the GameSparks SDK for your project.

## Setting Up and Connecting

*1.* The first step is to connect to your Game's backend. For this step you'll need your *API Key* and *Secret*, which you can get from the *Configurator > Overview* page of the portal.

*2.* Begin by requiring the necessary classes, we'll do this in the main.lua file:

```

local GS = require("GameSparks.GS")
local GSData = require('GameSparks.GSData')
local GSRequest = require('GameSparks.GSRequest')
local GSResponse = require('GameSparks.GSResponse')
local GSUtils = require('GameSparks.GSUtils')

```

*3.* You then create a function that outputs the information received and sent through GameSparks for debugging purposes. We'll call this function *writeText* and it will print a String variable:

```

local function writeText(string)
  print(string)
end

```

*4.* Next, we'll create a function which will update us if the GameSparks module succeeds or fails in connecting and we'll call the function *availabilityCallback* with a boolean parameter:

```

local function availabilityCallback(isAvailable)
writeText("Availability: " .. tostring(isAvailable) .. "\n")

  if isAvailable then
    --Do something
  end

end

```

The function will print the availability condition as well as perform any logic when the result of the condition is true or false. This is useful to determine if the GameSparks API is ready to use or not.

*5.* For the next step we'll be connecting to our Game's backend using the *API Key* and *Secret*:

```

--Create GS Instance
gs = createGS()
--Set the logger for debugging the Responses,Messages and Requests flowning in and out
gs.setLogger(writeText)
--Set API Key
gs.setApiKey("293711ZXWjA9")
--Set Secret
gs.setApiSecret("DgnYnPUE2D0RetwKAy5XPUxxxN7pl36e")
--Set availability callback function
gs.setAvailabilityCallback(availabilityCallback)
--Connect to your game's backend
gs.connect()


```

 Once you've run your project, the availability function will inform you if you're successfully connected:
 * If no output is shown from the function and your debugger is stuck in a connection loop then double-check your credentials (*API Key* and *Secret*) and check that you are connected to the internet.
 * Once you've successfully connected, you should get the message "Availability: True" in your output console.

In the next section we'll be learning how to [register and authenticate](/Getting Started/Using Authentication/README.md) users.
