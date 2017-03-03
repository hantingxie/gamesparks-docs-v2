
# ListLeaderboardsRequest


Returns a list of all leaderboards configured in the game.


<a href="https://api.gamesparks.net/#listleaderboardsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A response containing a list of all leaderboards configured in the game.

Parameter | Type | Description
--------- | ---- | -----------
leaderboards | [Leaderboard[]](#leaderboard) | A list of JSON object containing leaderboard meta data
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### Leaderboard

A nested object that represents the leaderboard configuration data.

Parameter | Type | Description
--------- | ---- | -----------
description | string | The leaderboard's description.
name | string | The leaderboard's name.
propertySet | JSON | The custom property set configured on this Leaderboard
shortCode | string | The leaderboard's short code.


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ListLeaderboardsRequest()
		.Send((response) => {
		GSEnumerable<var> leaderboards = response.Leaderboards; 
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
	    .createListLeaderboardsRequest()
		.send(function(response:com.gamesparks.api.responses.ListLeaderboardsResponse):void {
		var leaderboards:Vector.<Leaderboard> = response.getLeaderboards(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListLeaderboardsRequest* request = [[GSListLeaderboardsRequest alloc] init];
	[request setCallback:^ (GSListLeaderboardsResponse* response) {
	NSArray* leaderboards = [response getLeaderboards]; 
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
	
	void ListLeaderboardsRequest_Response(GS& gsInstance, const ListLeaderboardsResponse& response) {
	gsstl:vector<Types::Leaderboard*> leaderboards = response.getLeaderboards(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListLeaderboardsRequest request(gsInstance);
	request.Send(ListLeaderboardsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListLeaderboardsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListLeaderboardsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListLeaderboardsRequest()
	.send(new GSEventListener<ListLeaderboardsResponse>() {
		@Override
		public void onEvent(ListLeaderboardsResponse response) {
			List<Leaderboard> leaderboards = response.getLeaderboards(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListLeaderboardsRequest();
	var response = request.Send();
	
var leaderboards = response.leaderboards; 
var scriptData = response.scriptData; 
```


