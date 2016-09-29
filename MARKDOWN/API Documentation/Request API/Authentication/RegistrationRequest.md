
# RegistrationRequest


Allows a new player to be created using a username, password display name.


<a href="https://api.gamesparks.net/#registrationrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
displayName | Yes | string | A display name to use
password | Yes | string | The previously registered password
segments | No | JSON | An optional segment configuration for this request.
userName | Yes | string | The previously registered player name

## Response Parameters


A response to a registration request 

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
USERNAME | TAKEN | The userName supplied is already in use.

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new RegistrationRequest()
		.SetAnalyticsData(analyticsData)
		.SetDisplayName(displayName)
		.SetPassword(password)
		.SetSegments(segments)
		.SetUserName(userName)
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
	    .createRegistrationRequest()
		.setAnalyticsData(analyticsData)
		.setDisplayName(displayName)
		.setPassword(password)
		.setSegments(segments)
		.setUserName(userName)
		.send(function(response:com.gamesparks.api.responses.RegistrationResponse):void {
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
	GSRegistrationRequest* request = [[GSRegistrationRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setDisplayName:displayName;
	[request setPassword:password;
	[request setSegments:segments;
	[request setUserName:userName;
	[request setCallback:^ (GSRegistrationResponse* response) {
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
	
	void RegistrationRequest_Response(GS& gsInstance, const RegistrationResponse& response) {
	gsstl::string authToken = response.getAuthToken(); 
	gsstl::string displayName = response.getDisplayName(); 
	Optional::t_BoolOptional newPlayer = response.getNewPlayer(); 
	GSData scriptData = response.getScriptData(); 
	Types::Player* switchSummary = response.getSwitchSummary(); 
	gsstl::string userId = response.getUserId(); 
	}
	......
	
	RegistrationRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetDisplayName(displayName)
	request.SetPassword(password)
	request.SetSegments(segments)
	request.SetUserName(userName)
	request.Send(RegistrationRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.RegistrationRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.RegistrationResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createRegistrationRequest()
	.setAnalyticsData(analyticsData)
	.setDisplayName(displayName)
	.setPassword(password)
	.setSegments(segments)
	.setUserName(userName)
	.send(new GSEventListener<RegistrationResponse>() {
		@Override
		public void onEvent(RegistrationResponse response) {
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

	var request = new SparkRequests.RegistrationRequest();
	request.analyticsData = ...;
	request.displayName = ...;
	request.password = ...;
	request.segments = ...;
	request.userName = ...;
	var response = request.Send();
	
var authToken = response.authToken; 
var displayName = response.displayName; 
var newPlayer = response.newPlayer; 
var scriptData = response.scriptData; 
var switchSummary = response.switchSummary; 
var userId = response.userId; 
```


