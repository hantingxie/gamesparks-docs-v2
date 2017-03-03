---
src: /API Documentation/Request API/Teams/ListTeamsRequest.md
---

# ListTeamsRequest


Returns a list of teams. Can be filtered on team name or team type.


<a href="https://api.gamesparks.net/#listteamsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
entryCount | No | number | The number of teams to return in a page (default=50)
offset | No | number | The offset (page number) to start from (default=0)
teamNameFilter | No | string | An optional filter to return teams with a matching name
teamTypeFilter | No | string | An optional filter to return teams of a particular type

## Response Parameters


A response containing the list of teams for a game.

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
teams | [Team[]](#team) | A list of JSON objects containing team information

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

### Team

A nested object that represents the team. This object does not contain a list of the members.

Parameter | Type | Description
--------- | ---- | -----------
owner | [Player](#player) | A summary of the owner
teamId | string | The Id of the team
teamName | string | The team name
teamType | string | The team type


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ListTeamsRequest()
		.SetEntryCount(entryCount)
		.SetOffset(offset)
		.SetTeamNameFilter(teamNameFilter)
		.SetTeamTypeFilter(teamTypeFilter)
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
		GSEnumerable<var> teams = response.Teams; 
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
	    .createListTeamsRequest()
		.setEntryCount(entryCount)
		.setOffset(offset)
		.setTeamNameFilter(teamNameFilter)
		.setTeamTypeFilter(teamTypeFilter)
		.send(function(response:com.gamesparks.api.responses.ListTeamsResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var teams:Vector.<Team> = response.getTeams(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListTeamsRequest* request = [[GSListTeamsRequest alloc] init];
	[request setEntryCount:entryCount;
	[request setOffset:offset;
	[request setTeamNameFilter:teamNameFilter;
	[request setTeamTypeFilter:teamTypeFilter;
	[request setCallback:^ (GSListTeamsResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
	NSArray* teams = [response getTeams]; 
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
	
	void ListTeamsRequest_Response(GS& gsInstance, const ListTeamsResponse& response) {
	GSData scriptData = response.getScriptData(); 
	gsstl:vector<Types::Team*> teams = response.getTeams(); 
	}
	......
	
	ListTeamsRequest request(gsInstance);
	request.SetEntryCount(entryCount)
	request.SetOffset(offset)
	request.SetTeamNameFilter(teamNameFilter)
	request.SetTeamTypeFilter(teamTypeFilter)
	request.Send(ListTeamsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListTeamsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListTeamsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListTeamsRequest()
	.setEntryCount(entryCount)
	.setOffset(offset)
	.setTeamNameFilter(teamNameFilter)
	.setTeamTypeFilter(teamTypeFilter)
	.send(new GSEventListener<ListTeamsResponse>() {
		@Override
		public void onEvent(ListTeamsResponse response) {
			GSData scriptData = response.getScriptData(); 
			List<Team> teams = response.getTeams(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListTeamsRequest();
	request.entryCount = ...;
	request.offset = ...;
	request.teamNameFilter = ...;
	request.teamTypeFilter = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
var teams = response.teams; 
```


