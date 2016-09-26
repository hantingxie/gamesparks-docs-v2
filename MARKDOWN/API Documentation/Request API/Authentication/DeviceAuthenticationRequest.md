---
src: /API Documentation/Request API/Authentication/DeviceAuthenticationRequest.md
---

# DeviceAuthenticationRequest


Allows a device id to be used to create an anonymous profile in the game.

This allows the player to be tracked and have data stored against them before using FacebookConnectRequest to create a full profile.

DeviceAuthenticationRequest should not be used in conjunction with RegistrationRequest as the two accounts will not be merged.


<a href="https://api.gamesparks.net/#deviceauthenticationrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
deviceId | Yes | string | A unique device identifier. Each platform has it's own method for getting a unique id
deviceModel | No | string | The device model
deviceName | No | string | The device name
deviceOS | Yes | string | An indicator of the device platform, should be IOS, ANDROID, WP8 or W8
deviceType | No | string | The device type
displayName | No | string | An optional displayname for the player
operatingSystem | No | string | The device type
segments | No | JSON | An optional segment configuration for this request.

## Response Parameters


A response containing the auth token

Parameter | Type | Description
--------- | ---- | -----------
authToken | string | 44b297a8-162a-4220-8c14-dad9a1946ad2
displayName | string | The player's display name
newPlayer | boolean | Indicates whether the player was created as part of this request
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
switchSummary | [Player](#player) | A summary of the player that would be switched to.  Only returned as part of an error response for a request where automatic switching is disabled.
userId | string | The player's id

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### Player

A nested object that represents a player.

Parameter | Type | Description
--------- | ---- | -----------
achievements | string[] | The achievements of the Player
displayName | string | The display name of the Player
externalIds | JSON | The external Id's of the Player
id | string | The id of the Player
online | boolean | The online status of the Player
scriptData | JSON | The script data of the Player
virtualGoods | string[] | The virtual goods of the Player

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
deviceOS | IOS|ANDROID|WP8	 | The supplied deviceOS was not in the accepted range

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new DeviceAuthenticationRequest()
		.SetDeviceId(deviceId)
		.SetDeviceModel(deviceModel)
		.SetDeviceName(deviceName)
		.SetDeviceOS(deviceOS)
		.SetDeviceType(deviceType)
		.SetDisplayName(displayName)
		.SetOperatingSystem(operatingSystem)
		.SetSegments(segments)
		.Send((response) => {
		string authToken = response.AuthToken; 
		string displayName = response.DisplayName; 
		bool? newPlayer = response.NewPlayer; 
		GSData scriptData = response.ScriptData; 
		var switchSummary = response.SwitchSummary; 
		string userId = response.UserId; 
		});

```

### ActionScript 3
```actionscript
	import com.gamesparks.*;
	import com.gamesparks.api.requests.*;
	import com.gamesparks.api.responses.*;
	import com.gamesparks.api.types.*;
	...
	
	gs.getRequestBuilder()
	    .createDeviceAuthenticationRequest()
		.setDeviceId(deviceId)
		.setDeviceModel(deviceModel)
		.setDeviceName(deviceName)
		.setDeviceOS(deviceOS)
		.setDeviceType(deviceType)
		.setDisplayName(displayName)
		.setOperatingSystem(operatingSystem)
		.setSegments(segments)
		.send(function(response:com.gamesparks.api.responses.AuthenticationResponse):void {
		var authToken:String = response.getAuthToken(); 
		var displayName:String = response.getDisplayName(); 
		var newPlayer:Boolean = response.getNewPlayer(); 
		var scriptData:ScriptData = response.getScriptData(); 
		var switchSummary:Player = response.getSwitchSummary(); 
		var userId:String = response.getUserId(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSDeviceAuthenticationRequest* request = [[GSDeviceAuthenticationRequest alloc] init];
	[request setDeviceId:deviceId;
	[request setDeviceModel:deviceModel;
	[request setDeviceName:deviceName;
	[request setDeviceOS:deviceOS;
	[request setDeviceType:deviceType;
	[request setDisplayName:displayName;
	[request setOperatingSystem:operatingSystem;
	[request setSegments:segments;
	[request setCallback:^ (GSAuthenticationResponse* response) {
	NSString* authToken = [response getAuthToken]; 
	NSString* displayName = [response getDisplayName]; 
	BOOL newPlayer = [response getNewPlayer]; 
	NSDictionary* scriptData = [response getScriptData]; 
	GSPlayer* switchSummary = [response getSwitchSummary]; 
	NSString* userId = [response getUserId]; 
	}];
	[gs send:request];

```

### C++
```cpp

	#include <GameSparks/generated/GSRequests.h>
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Responses;
	using namespace GameSparks::Api::Requests;
	...
	
	void DeviceAuthenticationRequest_Response(GS& gsInstance, const AuthenticationResponse& response) {
	gsstl::string authToken = response.getAuthToken(); 
	gsstl::string displayName = response.getDisplayName(); 
	Optional::t_BoolOptional newPlayer = response.getNewPlayer(); 
	GSData scriptData = response.getScriptData(); 
	Types::Player* switchSummary = response.getSwitchSummary(); 
	gsstl::string userId = response.getUserId(); 
	}
	......
	
	DeviceAuthenticationRequest request(gsInstance);
	request.SetDeviceId(deviceId)
	request.SetDeviceModel(deviceModel)
	request.SetDeviceName(deviceName)
	request.SetDeviceOS(deviceOS)
	request.SetDeviceType(deviceType)
	request.SetDisplayName(displayName)
	request.SetOperatingSystem(operatingSystem)
	request.SetSegments(segments)
	request.Send(DeviceAuthenticationRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.DeviceAuthenticationRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AuthenticationResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createDeviceAuthenticationRequest()
	.setDeviceId(deviceId)
	.setDeviceModel(deviceModel)
	.setDeviceName(deviceName)
	.setDeviceOS(deviceOS)
	.setDeviceType(deviceType)
	.setDisplayName(displayName)
	.setOperatingSystem(operatingSystem)
	.setSegments(segments)
	.send(new GSEventListener<AuthenticationResponse>() {
		@Override
		public void onEvent(AuthenticationResponse response) {
			String authToken = response.getAuthToken(); 
			String displayName = response.getDisplayName(); 
			Boolean newPlayer = response.getNewPlayer(); 
			GSData scriptData = response.getScriptData(); 
			Player switchSummary = response.getSwitchSummary(); 
			String userId = response.getUserId(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.DeviceAuthenticationRequest();
	request.deviceId = ...;
	request.deviceModel = ...;
	request.deviceName = ...;
	request.deviceOS = ...;
	request.deviceType = ...;
	request.displayName = ...;
	request.operatingSystem = ...;
	request.segments = ...;
	var response = request.Send();
	
var authToken = response.authToken; 
var displayName = response.displayName; 
var newPlayer = response.newPlayer; 
var scriptData = response.scriptData; 
var switchSummary = response.switchSummary; 
var userId = response.userId; 
```


