---
src: /API Documentation/Request API/Multiplayer/MatchmakingRequest.md
---

# MatchmakingRequest


Register this player for matchmaking, using the given skill and matchShortCode.

Players looking for a match using the same matchShortCode will be considered for a match, based on the matchConfig.

Each player must match the other for the match to be found.

If the matchShortCode points to a match with realtime enabled, in order to minimise latency, the location of Players and their proximity to one another takes precedence over their reciprocal skill values.


<a href="https://api.gamesparks.net/#matchmakingrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
action | No | string | The action to take on the already in-flight request for this match. Currently supported actions are: 'cancel'
customQuery | No | JSON | The query that will be applied to the PendingMatch collection
matchData | No | JSON | A JSON Map of any data that will be associated to the pending match
matchGroup | No | string | Optional. Players will be grouped based on the distinct value passed in here, only players in the same group can be matched together
matchShortCode | Yes | string | The shortCode of the match type this player is registering for
participantData | No | JSON | A JSON Map of any data that will be associated to this user in a pending match
skill | No | number | The skill of the player looking for a match

## Response Parameters


A response to a matchmaking request

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
skill | may not be null | skill must be provided
matchShortCode | may not be null | matchShortCode must be provided
matchShortCode | NOT_FOUND | No matchConfig was found with the given matchShortCode
customQuery | INVALID_QUERY | No customQuery is not a valid mongo query
match | NOT_FOUND | No match was found for the current player

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new MatchmakingRequest()
		.SetAction(action)
		.SetCustomQuery(customQuery)
		.SetMatchData(matchData)
		.SetMatchGroup(matchGroup)
		.SetMatchShortCode(matchShortCode)
		.SetParticipantData(participantData)
		.SetSkill(skill)
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
	    .createMatchmakingRequest()
		.setAction(action)
		.setCustomQuery(customQuery)
		.setMatchData(matchData)
		.setMatchGroup(matchGroup)
		.setMatchShortCode(matchShortCode)
		.setParticipantData(participantData)
		.setSkill(skill)
		.send(function(response:com.gamesparks.api.responses.MatchmakingResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSMatchmakingRequest* request = [[GSMatchmakingRequest alloc] init];
	[request setAction:action;
	[request setCustomQuery:customQuery;
	[request setMatchData:matchData;
	[request setMatchGroup:matchGroup;
	[request setMatchShortCode:matchShortCode;
	[request setParticipantData:participantData;
	[request setSkill:skill;
	[request setCallback:^ (GSMatchmakingResponse* response) {
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
	
	void MatchmakingRequest_Response(GS& gsInstance, const MatchmakingResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	MatchmakingRequest request(gsInstance);
	request.SetAction(action)
	request.SetCustomQuery(customQuery)
	request.SetMatchData(matchData)
	request.SetMatchGroup(matchGroup)
	request.SetMatchShortCode(matchShortCode)
	request.SetParticipantData(participantData)
	request.SetSkill(skill)
	request.Send(MatchmakingRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.MatchmakingRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.MatchmakingResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createMatchmakingRequest()
	.setAction(action)
	.setCustomQuery(customQuery)
	.setMatchData(matchData)
	.setMatchGroup(matchGroup)
	.setMatchShortCode(matchShortCode)
	.setParticipantData(participantData)
	.setSkill(skill)
	.send(new GSEventListener<MatchmakingResponse>() {
		@Override
		public void onEvent(MatchmakingResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.MatchmakingRequest();
	request.action = ...;
	request.customQuery = ...;
	request.matchData = ...;
	request.matchGroup = ...;
	request.matchShortCode = ...;
	request.participantData = ...;
	request.skill = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


