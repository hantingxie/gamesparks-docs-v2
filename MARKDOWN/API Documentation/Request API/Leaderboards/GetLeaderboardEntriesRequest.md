---
src: /API Documentation/Request API/Leaderboards/GetLeaderboardEntriesRequest.md
---

# GetLeaderboardEntriesRequest


Get the leaderboard entry data for the current player or a given player. 

For each leaderboard it returns the hichest score the player has


<a href="https://api.gamesparks.net/#getleaderboardentriesrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challenges | No | string[] | The challenge leaderboards to return entries for
inverseSocial | No | boolean | Returns the leaderboard excluding the player's social friends
leaderboards | No | string[] | The list of leaderboards shortcodes
player | No | string | The player id. Leave out to use the current player id
social | No | boolean | Set to true to include the player's game friends
teamTypes | No | string[] | The types of team to apply this request to

## Response Parameters


A response containing leaderboard entry data for a given player

Parameter | Type | Description
--------- | ---- | -----------
results | JSON | The leaderboard entry data
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
	new GetLeaderboardEntriesRequest()
		.SetChallenges(challenges)
		.SetInverseSocial(inverseSocial)
		.SetLeaderboards(leaderboards)
		.SetPlayer(player)
		.SetSocial(social)
		.SetTeamTypes(teamTypes)
		.Send((response) => {
		GSData results = response.Results; 
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
	    .createGetLeaderboardEntriesRequest()
		.setChallenges(challenges)
		.setInverseSocial(inverseSocial)
		.setLeaderboards(leaderboards)
		.setPlayer(player)
		.setSocial(social)
		.setTeamTypes(teamTypes)
		.send(function(response:com.gamesparks.api.responses.GetLeaderboardEntriesResponse):void {
		var results:Object = response.getResults(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetLeaderboardEntriesRequest* request = [[GSGetLeaderboardEntriesRequest alloc] init];
	[request setChallenges:challenges;
	[request setInverseSocial:inverseSocial;
	[request setLeaderboards:leaderboards;
	[request setPlayer:player;
	[request setSocial:social;
	[request setTeamTypes:teamTypes;
	[request setCallback:^ (GSGetLeaderboardEntriesResponse* response) {
	NSDictionary* results = [response getResults]; 
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
	
	void GetLeaderboardEntriesRequest_Response(GS& gsInstance, const GetLeaderboardEntriesResponse& response) {
	GSData results = response.getResults(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	GetLeaderboardEntriesRequest request(gsInstance);
	request.SetChallenges(challenges)
	request.SetInverseSocial(inverseSocial)
	request.SetLeaderboards(leaderboards)
	request.SetPlayer(player)
	request.SetSocial(social)
	request.SetTeamTypes(teamTypes)
	request.Send(GetLeaderboardEntriesRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetLeaderboardEntriesRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetLeaderboardEntriesResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetLeaderboardEntriesRequest()
	.setChallenges(challenges)
	.setInverseSocial(inverseSocial)
	.setLeaderboards(leaderboards)
	.setPlayer(player)
	.setSocial(social)
	.setTeamTypes(teamTypes)
	.send(new GSEventListener<GetLeaderboardEntriesResponse>() {
		@Override
		public void onEvent(GetLeaderboardEntriesResponse response) {
			GSData results = response.getResults(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetLeaderboardEntriesRequest();
	request.challenges = ...;
	request.inverseSocial = ...;
	request.leaderboards = ...;
	request.player = ...;
	request.social = ...;
	request.teamTypes = ...;
	var response = request.Send();
	
var results = response.results; 
var scriptData = response.scriptData; 
```


