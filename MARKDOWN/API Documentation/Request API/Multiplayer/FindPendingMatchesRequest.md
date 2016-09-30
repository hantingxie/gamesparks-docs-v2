---
src: /API Documentation/Request API/Multiplayer/FindPendingMatchesRequest.md
---

# FindPendingMatchesRequest


Find other pending matches that will match this player's previously submitted MatchmakingRequest.

Used for manual matching of players, where you want control over which pending match should be chosen.

Each player must match the other for the pending match to be found.


<a href="https://api.gamesparks.net/#findpendingmatchesrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
matchGroup | No | string | Optional. The matchGroup of the match this player previously registeredfor
matchShortCode | Yes | string | The shortCode of the match this player previously registered for
maxMatchesToFind | No | number | Optional. The maximum number of pending matches to return (default=10)

## Response Parameters


A response to a FindPendingMatchesRequest

Parameter | Type | Description
--------- | ---- | -----------
pendingMatches | [PendingMatch[]](#pendingmatch) | A list of JSON objects containing pending matches
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### PendingMatch

An object that represents a pending match.

Parameter | Type | Description
--------- | ---- | -----------
id | string | The ID for the pending match
matchGroup | string | The match group for the pending match
matchShortCode | string | The match shortCode for the pending match
matchedPlayers | [MatchedPlayer[]](#matchedplayer) | The players already part of this pending match
skill | number | The average skill of players in this pending match

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### MatchedPlayer

An object that represents a player in a pending match.

Parameter | Type | Description
--------- | ---- | -----------
location | DBObject | The Location of the player
participantData | JSON | A JSON Map of any data that was associated to this user
playerId | string | The ID for player
skill | number | The skill of the player in this match

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
matchShortCode | may not be null | matchShortCode must be provided
matchShortCode | NOT_FOUND | No matchConfig was found with the given matchShortCode
match | NOT_IN_PROGRESS | There is no pending match for this player / shortCode / matchGroup currently in progress

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new FindPendingMatchesRequest()
		.SetAnalyticsData(analyticsData)
		.SetMatchGroup(matchGroup)
		.SetMatchShortCode(matchShortCode)
		.SetMaxMatchesToFind(maxMatchesToFind)
		.Send((response) => {
		GSEnumerable<var> pendingMatches = response.PendingMatches; 
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
	    .createFindPendingMatchesRequest()
		.setAnalyticsData(analyticsData)
		.setMatchGroup(matchGroup)
		.setMatchShortCode(matchShortCode)
		.setMaxMatchesToFind(maxMatchesToFind)
		.send(function(response:com.gamesparks.api.responses.FindPendingMatchesResponse):void {
		var pendingMatches:Vector.<PendingMatch> = response.getPendingMatches(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSFindPendingMatchesRequest* request = [[GSFindPendingMatchesRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setMatchGroup:matchGroup;
	[request setMatchShortCode:matchShortCode;
	[request setMaxMatchesToFind:maxMatchesToFind;
	[request setCallback:^ (GSFindPendingMatchesResponse* response) {
	NSArray* pendingMatches = [response getPendingMatches]; 
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
	
	void FindPendingMatchesRequest_Response(GS& gsInstance, const FindPendingMatchesResponse& response) {
	gsstl:vector<Types::PendingMatch*> pendingMatches = response.getPendingMatches(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	FindPendingMatchesRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetMatchGroup(matchGroup)
	request.SetMatchShortCode(matchShortCode)
	request.SetMaxMatchesToFind(maxMatchesToFind)
	request.Send(FindPendingMatchesRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.FindPendingMatchesRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.FindPendingMatchesResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createFindPendingMatchesRequest()
	.setAnalyticsData(analyticsData)
	.setMatchGroup(matchGroup)
	.setMatchShortCode(matchShortCode)
	.setMaxMatchesToFind(maxMatchesToFind)
	.send(new GSEventListener<FindPendingMatchesResponse>() {
		@Override
		public void onEvent(FindPendingMatchesResponse response) {
			List<PendingMatch> pendingMatches = response.getPendingMatches(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.FindPendingMatchesRequest();
	request.analyticsData = ...;
	request.matchGroup = ...;
	request.matchShortCode = ...;
	request.maxMatchesToFind = ...;
	var response = request.Send();
	
var pendingMatches = response.pendingMatches; 
var scriptData = response.scriptData; 
```


