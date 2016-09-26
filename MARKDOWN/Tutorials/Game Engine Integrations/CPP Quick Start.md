---
nav_sort: 1
src: /Tutorials/Game Engine Integrations/CPP Quick Start.md
---

# Cpp Quick Start

## Initialization

Include the following, each engine will have a slight variation:

```

//Include the headers for GS, IGSPlatform , the unique platform for the SDK and under the generated folder the headers for requests, responses and messages.
#include <GameSparks/GS.h>
#include <GameSparks/IGSPlatform.h>
#include <GameSparks/generated/GSRequests.h>
#include <GameSparks/generated/GSMessages.h>
#include <GameSparks/MarmaladePlatform.h>

//Add these namespaces
using namespace GameSparks::Core;
using namespace GameSparks::Api::Messages;
using namespace GameSparks::Api::Responses;
using namespace GameSparks::Api::Requests;

```

To use the platform you will have to create and connect the GS Module.

To create the module:

```
GameSparks::Core::GS GS;

```

Now to connect to the platform:

To do so for Marmalade:

```
MarmaladePlatform* gsPlatform= new MarmaladePlatform(apiKey, secret, usePreviewServerBool);

```

To do so for Cocos2d:

```

Cocos2dxPlatform* gsPlatform= new Cocos2dxPlatform(apikey, secret, usePreviewServerBool)

```

Then initialize the GS module using the connection:

```
GS.Initialise(&gsPlatform);

```

After the connection has been established the module will use the GameSparksAvailable function to issue a callback event:

```

//Set the callback event handler
GS.GameSparksAvailable = GameSparksAvailable;

//Then create a function to execute a sequence once the connection becomes available
void GameSparksAvailable(GameSparks::Core::GS& gsInstance, bool available)
{
	printf("GameSparks is %s\n", (available ? "available" : "not available"));

	if (available)
	{
	    // Do something immediately when gamesparks is available
	}
}

```

After connecting, you have the ability to use GameSpark requests to communicate with the platform. Many requests are denied if no player is authenticated. So an authentication request will be the first request made.

## Authentication

To authenticate a player in C++ you have three options for authentication:
* Username/password
* Device
* Social

### Username/Password Authentication

You can use the GameSparks username and password system - when a players use a registration request to register on the platform, they can use their credentials to log in.

Registration Request:

```

GameSparks::Api::Requests::RegistrationRequest request(gsInstance);
request.SetDisplayName("SDK Sample Test User");
request.SetUserName("abcdefgh");
request.SetDisplayName("abcdefgh");
request.SetPassword("abcdefgh");

// send the request
request.Send(RegistrationRequest_Response);

```

Registration Response:

```

void RegistrationRequest_Response(GameSparks::Core::GS& gsInstance, const GameSparks::Api::Responses::RegistrationResponse& response)
{
	if (response.GetHasErrors())
	{
		//Do something if unsuccessful
	}
	else
	{
		//Do something if successful
	}
}

```

Authentication Request:

```

GameSparks::Api::Requests::AuthenticationRequest request(gsInstance);
request.SetUserName("abcdefgh");
request.SetPassword("abcdefgh");

// send the request
request.Send(AuthenticationRequest_Response);

```

Authentication Response:

```

void AuthenticationRequest_Response(GameSparks::Core::GS& gsInstance, const GameSparks::Api::Responses::AuthenticationResponse& response)
{
	// If error
	if (response.GetHasErrors())
	{
          //Do something when unsuccessful
        }
        // If no error
        else
        {
          //DO something when successful
        }
}

```

### Device Authentication

You can authenticate a player using their device's unique ID and their device OS. The unique ID is a string value determined by the developer. Here's an example of device authentication request:

```

GameSparks::Api::Requests::DeviceAuthenticationRequest request(gsInstance);
request.SetDeviceId(deviceId);
request.SetDeviceOS(deviceOS);
request.Send(DeviceAuthenticationRequest_Response);

```

### Social Authentication


Using an Auth token, you can login the GameSparks platform using the information from a social media platform. Here's an example of how to make a social authentication using Facebook:

```

GameSparks::Api::Requests::FacebookConnectRequest request(gsInstance);
//Can use authentication token
request.SetAccessToken(token);
//Or can use authentication code
request.SetCode(code);
request.Send(FacebookConnectRequest_Response);

```

After authenticating, the user can now use other GameSparks requests and messages.

## Using Log Events and Cloud code

Log Events allow you to run custom logic coded in Cloud code. Cloud code is powerful, harnessing the power of JavaScript and the convenience of GameSparks API.

Here's an example of calling an event from C++ and passing in attribute values:

```

//Create an object to store float, boolean, int and string values and reference them using keys.
GSRequestData scriptData;

//Populate the object by assigning a key first, and a value. This key will be used to refer to the data in cloud code.
scriptData.AddString("exampleKey", "exampleValue");
scriptData.AddNumber("exampleKey2", 23);

//Create the log event request and refer to the correct event using the event key.
GameSparks::Api::Requests::LogEventRequest request(gsInstance);
request.SetEventKey("foo");
//Add input data you want to use in cloud code and send the request.
request.SetEventAttribute("objVal", scriptData);
request.SetEventAttribute("intVal", 23);
request.Send(fooEvent_Response);

```

Here's how to handle the response and retrieve output values. In our example we're trying to retrieve an object by referring to the object's key:

```

void fooEvent_Response(GameSparks::Core::GS& gsInstance, const GameSparks::Api::Responses::LogEventResponse response)
{
        //check for errors
	if (response.GetHasErrors())
	{

	}
	else
	{
    //If data exists, then do something with it. GetBaseData function extracts the data from the response.
		if (response.GetBaseData().GetGSDataObject("scriptData").GetValue().GetString("exampleKey").HasValue())
		{
			string val;
			val = response.GetBaseData().GetGSDataObject("scriptData").GetValue().GetString("exampleKey").GetValue();
		}
	}
}

```

To output a value from Cloud Code, use:

```

Spark.setScriptData("exampleKey", val);

```

To learn how to use Cloud Code and events, check out the [using Cloud Code](/Tutorials/Cloud Code and the Test Harness/Using Cloud Code.md) tutorial.


You can also augment your own requests with extra logic to suit your needs. To pass any input into a request you'll need to do this using 'scriptData'. For this example, we're going to send an E-Mail variable with the registration request to save an E-mail reference against our user.

```

//Create a data object
GSRequestData scriptData;
//Add a string variable with the key 'email'
scriptData.AddString("email", "example@gamesparks.com");

//Create a registration request
GameSparks::Api::Requests::RegistrationRequest request(gsInstance);
request.SetDisplayName("SDK Sample Test User");
request.SetUserName("abcdefgh");
request.SetDisplayName("abcdefgh");
//Insert the object as the scriptData
request.SetScriptData(scriptData);
request.SetPassword("abcdefgh");

// send the request
request.Send(RegistrationRequest_Response);

```

You can alter the way this request works using the Cloud Code section under *Bindings > Requests*, finding the *RegistrationRequest*, and adding in logic which saves the E-mail against the player. We have an [Automating User Password Change tutorial](/Tutorials/Social Authentication and Player Profile/Automating User Password Change.md) for this.
