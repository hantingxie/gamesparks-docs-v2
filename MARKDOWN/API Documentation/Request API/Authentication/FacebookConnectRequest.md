
# FacebookConnectRequest


Allows either a Facebook access token, or a Facebook authorization code to be used as an authentication mechanism.

Once authenticated the platform can determine the current players details from the Facebook platform and store them within GameSparks.

GameSparks will determine the player's friends and whether any of them are currently registered with the game.

If the Facebook user is already linked to a player, the current session will switch to the linked player.

If the current player has previously created an account using either DeviceAuthenticationRequest or RegistrationRequest AND the Facebook user is not already registered with the game, the Facebook user will be linked to the current player.

If the current player has not authenticated and the Facebook user is not known, a new player will be created using the Facebook details and the session will be authenticated against the new player.

If the Facebook user is already known, the session will switch to being the previously created user.


<a href="https://api.gamesparks.net/#facebookconnectrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
accessToken | No | string | The access token is used by the client to make authenticated requests on behalf of the end user.
analyticsData | No | AnalyticsData | Optional data used by analytics
code | No | string | An authorization code is a short-lived token representing the user's access grant, created by the authorization server and passed to the client application via the browser.
doNotLinkToCurrentPlayer | No | boolean | Indicates that the server should not try to link the external profile with the current player.  If false, links the external profile to the currently signed in player.  If true, creates a new player and links the external profile to them.  Defaults to false.
errorOnSwitch | No | boolean | Indicates whether the server should return an error if an account switch would have occurred, rather than switching automatically.  Defaults to false.
segments | No | JSON | An optional segment configuration for this request.
switchIfPossible | No | boolean | Indicates that the server should switch to the supplied profile if it isalready associated to a player. Defaults to false.
syncDisplayName | No | boolean | Indicates that the associated players displayName should be kept in syn with this profile when it's updated by the external provider.

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
accessToken | ACCOUNT_ALREADY_LINKED | The current user has a Facebook profile and it's not the profile they have just tried to log in with
code | NOTAUTHENTICATED | The system was unable to authenticate the code
accessToken | NOTAUTHENTICATED | The system was unable to authenticate the token
accessToken | REQUIRED | Both the code and the accessToken are missing

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new FacebookConnectRequest()
		.SetAccessToken(accessToken)
		.SetAnalyticsData(analyticsData)
		.SetCode(code)
		.SetDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
		.SetErrorOnSwitch(errorOnSwitch)
		.SetSegments(segments)
		.SetSwitchIfPossible(switchIfPossible)
		.SetSyncDisplayName(syncDisplayName)
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
	    .createFacebookConnectRequest()
		.setAccessToken(accessToken)
		.setAnalyticsData(analyticsData)
		.setCode(code)
		.setDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
		.setErrorOnSwitch(errorOnSwitch)
		.setSegments(segments)
		.setSwitchIfPossible(switchIfPossible)
		.setSyncDisplayName(syncDisplayName)
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
	GSFacebookConnectRequest* request = [[GSFacebookConnectRequest alloc] init];
	[request setAccessToken:accessToken;
	[request setAnalyticsData:analyticsData;
	[request setCode:code;
	[request setDoNotLinkToCurrentPlayer:doNotLinkToCurrentPlayer;
	[request setErrorOnSwitch:errorOnSwitch;
	[request setSegments:segments;
	[request setSwitchIfPossible:switchIfPossible;
	[request setSyncDisplayName:syncDisplayName;
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
	
	void FacebookConnectRequest_Response(GS& gsInstance, const AuthenticationResponse& response) {
	gsstl::string authToken = response.getAuthToken(); 
	gsstl::string displayName = response.getDisplayName(); 
	Optional::t_BoolOptional newPlayer = response.getNewPlayer(); 
	GSData scriptData = response.getScriptData(); 
	Types::Player* switchSummary = response.getSwitchSummary(); 
	gsstl::string userId = response.getUserId(); 
	}
	......
	
	FacebookConnectRequest request(gsInstance);
	request.SetAccessToken(accessToken)
	request.SetAnalyticsData(analyticsData)
	request.SetCode(code)
	request.SetDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
	request.SetErrorOnSwitch(errorOnSwitch)
	request.SetSegments(segments)
	request.SetSwitchIfPossible(switchIfPossible)
	request.SetSyncDisplayName(syncDisplayName)
	request.Send(FacebookConnectRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.FacebookConnectRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AuthenticationResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createFacebookConnectRequest()
	.setAccessToken(accessToken)
	.setAnalyticsData(analyticsData)
	.setCode(code)
	.setDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
	.setErrorOnSwitch(errorOnSwitch)
	.setSegments(segments)
	.setSwitchIfPossible(switchIfPossible)
	.setSyncDisplayName(syncDisplayName)
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

	var request = new SparkRequests.FacebookConnectRequest();
	request.accessToken = ...;
	request.analyticsData = ...;
	request.code = ...;
	request.doNotLinkToCurrentPlayer = ...;
	request.errorOnSwitch = ...;
	request.segments = ...;
	request.switchIfPossible = ...;
	request.syncDisplayName = ...;
	var response = request.Send();
	
var authToken = response.authToken; 
var displayName = response.displayName; 
var newPlayer = response.newPlayer; 
var scriptData = response.scriptData; 
var switchSummary = response.switchSummary; 
var userId = response.userId; 
```


