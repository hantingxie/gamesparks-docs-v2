---
nav_sort: 5
src: /Getting Started/Using Authentication/Lua Authentication.md
---

# Lua Authentication

There are three ways to authenticate using GameSparks:

1. GameSparks Authentication - Uses a username/password that players register to.
2. Device Authentication - Uses a unique string ID (created by the Developer) and an OS identifier.
3. Social authentication - Requires you to use a token from the social provider to authenticate users using the information gathered from their profiles.

In this tutorial we'll only cover GameSparks and Device authentication because Social authentication is different for every provider and that is beyond the scope of this tutorial.

## GameSparks Authentication

First you will need to register your user by providing *DisplayName*, *Username* and *Password*.

Create a registration request and set the values necessary for registration. This example has hard set values and for your game you'll need to have your players input these values:

```
--Build request
local requestBuilder = gs.getRequestBuilder()
local registerRequest = requestBuilder.createRegistrationRequest()

--Set values
registerRequest:setDisplayName("examplePlayer")
registerRequest:setUserName("exampleUsername")
registerRequest:setPassword("password")

--Send and check for errors, if no errors print username and message
registerRequest:send(function(authenticationResponse)
    if not authenticationResponse:hasErrors() then
    print(response:getUserName() " has successfully registered!")
    end
end)

```

Once registered, the player can now use their credentials to log in. When a player registers they are automatically signed in, there's no need to authenticate again. However, in this tutorial we'll demonstrate the authentication request.

To set this up, create an authentication request and input the values you used to register:

```
--Build request
local requestBuilder = gs.getRequestBuilder()
local loginAuth = requestBuilder.createAuthenticationRequest()

--Set values    
loginAuth:setPassword("pass")
loginAuth:setUserName("gstest")

--Send and check for errors, if there are errors print them
loginAuth:send(function(authenticationResponse)
if authenticationResponse:hasErrors() then
   	for key,value in pairs(authenticationResponse:getErrors()) do print(key,value) end
   end
end)

```

## Device Authentication

Device authentication doesn't need registration and relies on the Device ID (Needs to be unique) and the Device OS - can also be used as for other things - in this example we mark the OS as Corona:

```
--Build request
local requestBuilder = gs.getRequestBuilder()
local deviceAuthenticationRequest = requestBuilder.createDeviceAuthenticationRequest()

--Set values
deviceAuthenticationRequest:setDeviceId("1111")
deviceAuthenticationRequest:setDeviceOS("Corona")

--Send and print authentication token
deviceAuthenticationRequest:send(function(authenticationResponse)
writeText("token: "..authenticationResponse:getAuthToken().."\n")
end)
```

Authenticated players can also be linked to social accounts once created. A player that authenticated via Device Authentication can decide to link their social account to their user and use their social credential to login in the future.

Once a player authenticates they can now make requests and use GameSparks.

The [next tutorial](/Getting Started/Using Cloud Code/Lua Cloud Code.md) will demonstrate creating and using custom functions and using persistent data.
