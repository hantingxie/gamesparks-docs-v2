---
src: /API Documentation/Request API/Authentication/GooglePlayConnectRequest.md
---

# GooglePlayConnectRequest


Allows either a Google Play access code or an access token to be used as an authentication mechanism.

The access code needs to have at least the https://www.googleapis.com/auth/games scope.

For more details about Google OAuth 2.0 scopes refer to this: https://developers.google.com/identity/protocols/googlescopes#gamesConfigurationv1configuration

If the Google Play user is already linked to a player, the current session will switch to the linked player.

If the current player has previously created an account using either DeviceAuthentictionRequest or RegistrationRequest AND the Google Play user is not already registered with the game, the Google Play user will be linked to the current player.

If the current player has not authenticated and the Google Play user is not known, a new player will be created using the Google Play details and the session will be authenticated against the new player.

If the Google Play user is already known, the session will switch to being the previously created user.


<a href="https://api.gamesparks.net/#googleplayconnectrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
accessToken | No | string | The access token is used when using the service id and certificate.
code | No | string | The access code is used by the client to make authenticated requests on behalf of the end user. Requires clientId and clientsecret to be set
displayName | No | string | The display of the current player from Google Play. This will be used as the displayName of the gamesparks player if created (or syncDisplayname is true)
doNotLinkToCurrentPlayer | No | boolean | Indicates that the server should not try to link the external profile with the current player.  If false, links the external profile to the currently signed in player.  If true, creates a new player and links the external profile to them.  Defaults to false.
errorOnSwitch | No | boolean | Indicates whether the server should return an error if an account switch would have occurred, rather than switching automatically.  Defaults to false.
googlePlusScope | No | boolean | Did you request the plus.login scope when you got the access code or authorisation token from Google? If this is true, we will fetch the user's google+ account and friends
profileScope | No | boolean | Did you request the profile scope when you got the access code or authorisation token from Google? If this is true, we will fetch the user info by calling https://www.googleapis.com/oauth2/v1/userinfo?alt=json 
redirectUri | No | string | Only required when the access code has been granted using an explicit redirectUri, for example when using the mechanism described in https://developers.google.com/+/web/signin/server-side-flow
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
code | NOTAUTHENTICATED | The system was unable to authenticate the code
accessToken&#124;code | REQUIRED | Both the code and the accessToken are missing
displayName | REQUIRED | The displayName is missing
GOOGLE_PLAY | NOT_CONFIGURED | The game has not been configured with the required Google Play App ID
GOOGLE_PLUS | NOT_CONFIGURED | Google+ scope is requested, but the game has not been configured with the required Google Plus integration credentials: the client ID and the client secret
redirectUri | REQUIRED | The redirectUri is required when using a code rather than an accessToken
authentication | COPPA restricted | Social authentications are not allowed on COPPA compliant credentials due to social accounts containing personally identifiable information

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GooglePlayConnectRequest()
		.SetAccessToken(accessToken)
		.SetCode(code)
		.SetDisplayName(displayName)
		.SetDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
		.SetErrorOnSwitch(errorOnSwitch)
		.SetGooglePlusScope(googlePlusScope)
		.SetProfileScope(profileScope)
		.SetRedirectUri(redirectUri)
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
	    .createGooglePlayConnectRequest()
		.setAccessToken(accessToken)
		.setCode(code)
		.setDisplayName(displayName)
		.setDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
		.setErrorOnSwitch(errorOnSwitch)
		.setGooglePlusScope(googlePlusScope)
		.setProfileScope(profileScope)
		.setRedirectUri(redirectUri)
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
	GSGooglePlayConnectRequest* request = [[GSGooglePlayConnectRequest alloc] init];
	[request setAccessToken:accessToken;
	[request setCode:code;
	[request setDisplayName:displayName;
	[request setDoNotLinkToCurrentPlayer:doNotLinkToCurrentPlayer;
	[request setErrorOnSwitch:errorOnSwitch;
	[request setGooglePlusScope:googlePlusScope;
	[request setProfileScope:profileScope;
	[request setRedirectUri:redirectUri;
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
	
	void GooglePlayConnectRequest_Response(GS& gsInstance, const AuthenticationResponse& response) {
	gsstl::string authToken = response.getAuthToken(); 
	gsstl::string displayName = response.getDisplayName(); 
	Optional::t_BoolOptional newPlayer = response.getNewPlayer(); 
	GSData scriptData = response.getScriptData(); 
	Types::Player* switchSummary = response.getSwitchSummary(); 
	gsstl::string userId = response.getUserId(); 
	}
	......
	
	GooglePlayConnectRequest request(gsInstance);
	request.SetAccessToken(accessToken)
	request.SetCode(code)
	request.SetDisplayName(displayName)
	request.SetDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
	request.SetErrorOnSwitch(errorOnSwitch)
	request.SetGooglePlusScope(googlePlusScope)
	request.SetProfileScope(profileScope)
	request.SetRedirectUri(redirectUri)
	request.SetSegments(segments)
	request.SetSwitchIfPossible(switchIfPossible)
	request.SetSyncDisplayName(syncDisplayName)
	request.Send(GooglePlayConnectRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GooglePlayConnectRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AuthenticationResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGooglePlayConnectRequest()
	.setAccessToken(accessToken)
	.setCode(code)
	.setDisplayName(displayName)
	.setDoNotLinkToCurrentPlayer(doNotLinkToCurrentPlayer)
	.setErrorOnSwitch(errorOnSwitch)
	.setGooglePlusScope(googlePlusScope)
	.setProfileScope(profileScope)
	.setRedirectUri(redirectUri)
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

	var request = new SparkRequests.GooglePlayConnectRequest();
	request.accessToken = ...;
	request.code = ...;
	request.displayName = ...;
	request.doNotLinkToCurrentPlayer = ...;
	request.errorOnSwitch = ...;
	request.googlePlusScope = ...;
	request.profileScope = ...;
	request.redirectUri = ...;
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


