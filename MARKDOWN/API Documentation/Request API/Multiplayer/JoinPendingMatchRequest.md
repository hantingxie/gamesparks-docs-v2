
# JoinPendingMatchRequest


Requests to join a pending match (found via FindPendingMatchesRequest).


<a href="https://api.gamesparks.net/#joinpendingmatchrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
matchGroup | No | string | Optional. The matchGroup of the match this player previously registeredfor
matchShortCode | Yes | string | The shortCode of the match this player previously registered for
pendingMatchId | Yes | string | The pending match ID to join

## Response Parameters


A response to a JoinPendingMatchRequest

Parameter | Type | Description
--------- | ---- | -----------
pendingMatch | [PendingMatch](#pendingmatch) | A JSON object containing the new pending match
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
pendingMatchId | NOT_AVAILABLE | The requested pending match ID is not available to be joined

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new JoinPendingMatchRequest()
		.SetAnalyticsData(analyticsData)
		.SetMatchGroup(matchGroup)
		.SetMatchShortCode(matchShortCode)
		.SetPendingMatchId(pendingMatchId)
		.Send((response) => {
		var pendingMatch = response.PendingMatch; 
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
	    .createJoinPendingMatchRequest()
		.setAnalyticsData(analyticsData)
		.setMatchGroup(matchGroup)
		.setMatchShortCode(matchShortCode)
		.setPendingMatchId(pendingMatchId)
		.send(function(response:com.gamesparks.api.responses.JoinPendingMatchResponse):void {
		var pendingMatch:PendingMatch = response.getPendingMatch(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSJoinPendingMatchRequest* request = [[GSJoinPendingMatchRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setMatchGroup:matchGroup;
	[request setMatchShortCode:matchShortCode;
	[request setPendingMatchId:pendingMatchId;
	[request setCallback:^ (GSJoinPendingMatchResponse* response) {
	GSPendingMatch* pendingMatch = [response getPendingMatch]; 
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
	
	void JoinPendingMatchRequest_Response(GS& gsInstance, const JoinPendingMatchResponse& response) {
	Types::PendingMatch* pendingMatch = response.getPendingMatch(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	JoinPendingMatchRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetMatchGroup(matchGroup)
	request.SetMatchShortCode(matchShortCode)
	request.SetPendingMatchId(pendingMatchId)
	request.Send(JoinPendingMatchRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.JoinPendingMatchRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.JoinPendingMatchResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createJoinPendingMatchRequest()
	.setAnalyticsData(analyticsData)
	.setMatchGroup(matchGroup)
	.setMatchShortCode(matchShortCode)
	.setPendingMatchId(pendingMatchId)
	.send(new GSEventListener<JoinPendingMatchResponse>() {
		@Override
		public void onEvent(JoinPendingMatchResponse response) {
			PendingMatch pendingMatch = response.getPendingMatch(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.JoinPendingMatchRequest();
	request.analyticsData = ...;
	request.matchGroup = ...;
	request.matchShortCode = ...;
	request.pendingMatchId = ...;
	var response = request.Send();
	
var pendingMatch = response.pendingMatch; 
var scriptData = response.scriptData; 
```


