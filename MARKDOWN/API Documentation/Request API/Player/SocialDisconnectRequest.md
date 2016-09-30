---
src: /API Documentation/Request API/Player/SocialDisconnectRequest.md
---

# SocialDisconnectRequest


Allows a player's internal profile to be disconnected from an external system to which it is linked.  Any friends linked as result of this connection will be removed.


<a href="https://api.gamesparks.net/#socialdisconnectrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
systemId | No | string | The external system from which to disconnect this profile, supplied as a two letter ID. The options are: {FACEBOOK:FB, AMAZON:AM, GAME_CENTER:GC

## Response Parameters


A response to a SocialDisconnectRequest

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
systemId | REQUIRED | A systemId from which to disconnect must be provided
systemId | NOT_CONNECTED | The player does not have a connection with the provided system.
userName | CHANGE_REQUIRED | If the player's userName was derived from the profile they are disconnecting from, they must change it before they can disconnect.  The userName can be changed via a ChangeUserDetailsRequest.
password | NOT_SET | Before disconnecting, if the player has no other connected profiles then they must have a password set in order to be able to authenticate in the future.  A password can be set via a ChangeUserDetailsRequest.

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new SocialDisconnectRequest()
		.SetAnalyticsData(analyticsData)
		.SetSystemId(systemId)
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
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
	    .createSocialDisconnectRequest()
		.setAnalyticsData(analyticsData)
		.setSystemId(systemId)
		.send(function(response:com.gamesparks.api.responses.SocialDisconnectResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSSocialDisconnectRequest* request = [[GSSocialDisconnectRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setSystemId:systemId;
	[request setCallback:^ (GSSocialDisconnectResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
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
	
	void SocialDisconnectRequest_Response(GS& gsInstance, const SocialDisconnectResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	SocialDisconnectRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetSystemId(systemId)
	request.Send(SocialDisconnectRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.SocialDisconnectRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.SocialDisconnectResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createSocialDisconnectRequest()
	.setAnalyticsData(analyticsData)
	.setSystemId(systemId)
	.send(new GSEventListener<SocialDisconnectResponse>() {
		@Override
		public void onEvent(SocialDisconnectResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.SocialDisconnectRequest();
	request.analyticsData = ...;
	request.systemId = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


