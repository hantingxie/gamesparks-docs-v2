
# GameCenterConnectRequest


Allows an Apple account that has GameCenter to be used as an authentication mechanism.

The request must supply the GameCenter user details, such as the player id and username.

If the GameCenter user is already linked to a player, the current session will switch to the linked player.

If the current player has previously created an account using either DeviceAuthentictionRequest or RegistrationRequest AND the GameCenter user is not already registered with the game, the GameCenter user will be linked to the current player.

If the current player has not authenticated and the GameCenter user is not known, a new player will be created using the GameCenter details and the session will be authenticated against the new player.

If the GameCenter user is already known, the session will switch to being the previously created user.

This API call requires the output details from GKLocalPlayer.generateIdentityVerificationSignatureWithCompletionHandler on your iOS device


<a href="https://api.gamesparks.net/#gamecenterconnectrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
displayName | No | string | The display of the current player from GameCenter. This will be used as the displayName of the gamesparks player if created (or syncDisplayname is true)
doNotLinkToCurrentPlayer | No | boolean | Indicates that the server should not try to link the external profile with the current player.  If false, links the external profile to the currently signed in player.  If true, creates a new player and links the external profile to them.  Defaults to false.
errorOnSwitch | No | boolean | Indicates whether the server should return an error if an account switch would have occurred, rather than switching automatically.  Defaults to false.
externalPlayerId | No | string | The game center id of the current player. This value obtained be obtained from GKLocalPlayer playerID
publicKeyUrl | No | string | The url from where we will download the public key. This value should be obtained from generateIdentityVerificationSignatureWithCompletionHandler. 
salt | No | string | The salt is needed in order to prevent request forgery. This value should be obtained from generateIdentityVerificationSignatureWithCompletionHandler and should be base64 encoded using [salt base64Encoding]
segments | No | JSON | An optional segment configuration for this request.
signature | No | string | The signature is needed to validate that the request is genuine and that we can save the player. This value should be obtained from generateIdentityVerificationSignatureWithCompletionHandler and should be base64 encoded using [signature base64Encoding]
switchIfPossible | No | boolean | Indicates that the server should switch to the supplied profile if it isalready associated to a player. Defaults to false.
syncDisplayName | No | boolean | Indicates that the associated players displayName should be kept in syn with this profile when it's updated by the external provider.
timestamp | No | number | The timestamp is needed to validate the request signature. This value should be obtained from generateIdentityVerificationSignatureWithCompletionHandler

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
externalPlayerId | ACCOUNT_ALREADY_LINKED | The current user has a GameCenter profile and it's not the profile they have just tried to log in with
signature | NOTAUTHENTICATED | The system was unable to validate the request
externalPlayerId | NOTAUTHENTICATED | The system was unable to validate the external player ID
publicKeyUrl | REQUIRED | The publicKeyUrl is required but not provided
timestamp | REQUIRED | The timestamp is required but not provided
timestamp | EXPIRED | The request expired
signature | REQUIRED | The signature is required but not provided
salt | REQUIRED | The salt is required but not provided
externalPlayerId | REQUIRED | The externalPlayerId is required but not provided
displayName | REQUIRED | The displayName is required but not provided

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GameCenterConnectRequest()
		.SetAnalyticsData(analyticsData)
		.SetDisplayName(displayName)
		.SetDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
		.SetErrorOnSwitch(errorOnSwitch)
		.SetExternalPlayerId(externalPlayerId)
		.SetPublicKeyUrl(publicKeyUrl)
		.SetSalt(salt)
		.SetSegments(segments)
		.SetSignature(signature)
		.SetSwitchIfPossible(switchIfPossible)
		.SetSyncDisplayName(syncDisplayName)
		.SetTimestamp(timestamp)
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
	    .createGameCenterConnectRequest()
		.setAnalyticsData(analyticsData)
		.setDisplayName(displayName)
		.setDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
		.setErrorOnSwitch(errorOnSwitch)
		.setExternalPlayerId(externalPlayerId)
		.setPublicKeyUrl(publicKeyUrl)
		.setSalt(salt)
		.setSegments(segments)
		.setSignature(signature)
		.setSwitchIfPossible(switchIfPossible)
		.setSyncDisplayName(syncDisplayName)
		.setTimestamp(timestamp)
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
	GSGameCenterConnectRequest* request = [[GSGameCenterConnectRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setDisplayName:displayName;
	[request setDoNotLinkToCurrentPlayer:doNotLinkToCurrentPlayer;
	[request setErrorOnSwitch:errorOnSwitch;
	[request setExternalPlayerId:externalPlayerId;
	[request setPublicKeyUrl:publicKeyUrl;
	[request setSalt:salt;
	[request setSegments:segments;
	[request setSignature:signature;
	[request setSwitchIfPossible:switchIfPossible;
	[request setSyncDisplayName:syncDisplayName;
	[request setTimestamp:timestamp;
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
	
	void GameCenterConnectRequest_Response(GS& gsInstance, const AuthenticationResponse& response) {
	gsstl::string authToken = response.getAuthToken(); 
	gsstl::string displayName = response.getDisplayName(); 
	Optional::t_BoolOptional newPlayer = response.getNewPlayer(); 
	GSData scriptData = response.getScriptData(); 
	Types::Player* switchSummary = response.getSwitchSummary(); 
	gsstl::string userId = response.getUserId(); 
	}
	......
	
	GameCenterConnectRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetDisplayName(displayName)
	request.SetDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
	request.SetErrorOnSwitch(errorOnSwitch)
	request.SetExternalPlayerId(externalPlayerId)
	request.SetPublicKeyUrl(publicKeyUrl)
	request.SetSalt(salt)
	request.SetSegments(segments)
	request.SetSignature(signature)
	request.SetSwitchIfPossible(switchIfPossible)
	request.SetSyncDisplayName(syncDisplayName)
	request.SetTimestamp(timestamp)
	request.Send(GameCenterConnectRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GameCenterConnectRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AuthenticationResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGameCenterConnectRequest()
	.setAnalyticsData(analyticsData)
	.setDisplayName(displayName)
	.setDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
	.setErrorOnSwitch(errorOnSwitch)
	.setExternalPlayerId(externalPlayerId)
	.setPublicKeyUrl(publicKeyUrl)
	.setSalt(salt)
	.setSegments(segments)
	.setSignature(signature)
	.setSwitchIfPossible(switchIfPossible)
	.setSyncDisplayName(syncDisplayName)
	.setTimestamp(timestamp)
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

	var request = new SparkRequests.GameCenterConnectRequest();
	request.analyticsData = ...;
	request.displayName = ...;
	request.doNotLinkToCurrentPlayer = ...;
	request.errorOnSwitch = ...;
	request.externalPlayerId = ...;
	request.publicKeyUrl = ...;
	request.salt = ...;
	request.segments = ...;
	request.signature = ...;
	request.switchIfPossible = ...;
	request.syncDisplayName = ...;
	request.timestamp = ...;
	var response = request.Send();
	
var authToken = response.authToken; 
var displayName = response.displayName; 
var newPlayer = response.newPlayer; 
var scriptData = response.scriptData; 
var switchSummary = response.switchSummary; 
var userId = response.userId; 
```


