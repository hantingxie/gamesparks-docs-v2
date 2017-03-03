---
src: /API Documentation/Request API/Teams/GetMyTeamsRequest.md
---

# GetMyTeamsRequest


Get the teams that the player is in. Can be filtered on team type and also on those teams that the player owns.


<a href="https://api.gamesparks.net/#getmyteamsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
ownedOnly | No | boolean | Set to true to only get teams owned by the player
teamTypes | No | string[] | The type of teams to get

## Response Parameters


A response containing team data for teams that a player belong to

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
teams | [Team[]](#team) | The team data

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

A nested object that represents the team.

Parameter | Type | Description
--------- | ---- | -----------
members | [Player[]](#player) | The team members
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
	new GetMyTeamsRequest()
		.SetOwnedOnly(ownedOnly)
		.SetTeamTypes(teamTypes)
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
	    .createGetMyTeamsRequest()
		.setOwnedOnly(ownedOnly)
		.setTeamTypes(teamTypes)
		.send(function(response:com.gamesparks.api.responses.GetMyTeamsResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var teams:Vector.<Team> = response.getTeams(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetMyTeamsRequest* request = [[GSGetMyTeamsRequest alloc] init];
	[request setOwnedOnly:ownedOnly;
	[request setTeamTypes:teamTypes;
	[request setCallback:^ (GSGetMyTeamsResponse* response) {
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
	
	void GetMyTeamsRequest_Response(GS& gsInstance, const GetMyTeamsResponse& response) {
	GSData scriptData = response.getScriptData(); 
	gsstl:vector<Types::Team*> teams = response.getTeams(); 
	}
	......
	
	GetMyTeamsRequest request(gsInstance);
	request.SetOwnedOnly(ownedOnly)
	request.SetTeamTypes(teamTypes)
	request.Send(GetMyTeamsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetMyTeamsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetMyTeamsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetMyTeamsRequest()
	.setOwnedOnly(ownedOnly)
	.setTeamTypes(teamTypes)
	.send(new GSEventListener<GetMyTeamsResponse>() {
		@Override
		public void onEvent(GetMyTeamsResponse response) {
			GSData scriptData = response.getScriptData(); 
			List<Team> teams = response.getTeams(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetMyTeamsRequest();
	request.ownedOnly = ...;
	request.teamTypes = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
var teams = response.teams; 
```


