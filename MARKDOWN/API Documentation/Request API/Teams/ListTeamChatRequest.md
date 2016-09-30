---
src: /API Documentation/Request API/Teams/ListTeamChatRequest.md
---

# ListTeamChatRequest


Get a list of the messages sent to the team (by players using SendTeamChatMessageRequest).


<a href="https://api.gamesparks.net/#listteamchatrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
entryCount | No | number | The number of messages to return (default=50)
offset | No | number | The offset (nth message) to start from (default=0)
ownerId | No | string | The team owner to find, used in combination with teamType. If not supplied the current players id will be used
teamId | No | string | The teamId to find (may be null if teamType supplied)
teamType | No | string | The teamType to find, used in combination with the current player, or the player defined by ownerId

## Response Parameters


A response to a list team messages request.

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


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ListTeamChatRequest()
		.SetAnalyticsData(analyticsData)
		.SetEntryCount(entryCount)
		.SetOffset(offset)
		.SetOwnerId(ownerId)
		.SetTeamId(teamId)
		.SetTeamType(teamType)
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
	    .createListTeamChatRequest()
		.setAnalyticsData(analyticsData)
		.setEntryCount(entryCount)
		.setOffset(offset)
		.setOwnerId(ownerId)
		.setTeamId(teamId)
		.setTeamType(teamType)
		.send(function(response:com.gamesparks.api.responses.ListTeamChatResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListTeamChatRequest* request = [[GSListTeamChatRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setEntryCount:entryCount;
	[request setOffset:offset;
	[request setOwnerId:ownerId;
	[request setTeamId:teamId;
	[request setTeamType:teamType;
	[request setCallback:^ (GSListTeamChatResponse* response) {
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
	
	void ListTeamChatRequest_Response(GS& gsInstance, const ListTeamChatResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListTeamChatRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetEntryCount(entryCount)
	request.SetOffset(offset)
	request.SetOwnerId(ownerId)
	request.SetTeamId(teamId)
	request.SetTeamType(teamType)
	request.Send(ListTeamChatRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListTeamChatRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListTeamChatResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListTeamChatRequest()
	.setAnalyticsData(analyticsData)
	.setEntryCount(entryCount)
	.setOffset(offset)
	.setOwnerId(ownerId)
	.setTeamId(teamId)
	.setTeamType(teamType)
	.send(new GSEventListener<ListTeamChatResponse>() {
		@Override
		public void onEvent(ListTeamChatResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListTeamChatRequest();
	request.analyticsData = ...;
	request.entryCount = ...;
	request.offset = ...;
	request.ownerId = ...;
	request.teamId = ...;
	request.teamType = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


