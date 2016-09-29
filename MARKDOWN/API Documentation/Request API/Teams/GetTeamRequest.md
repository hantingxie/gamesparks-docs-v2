
# GetTeamRequest


Allows the details of a team to be retrieved.


<a href="https://api.gamesparks.net/#getteamrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
ownerId | No | string | The team owner to find, used in combination with teamType. If not supplied the current players id will be used
teamId | No | string | The teamId to find (may be null if teamType supplied)
teamType | No | string | The teamType to find, used in combination with the current player, or the player defined by ownerId

## Response Parameters


A response containing the details of the requested teams

Parameter | Type | Description
--------- | ---- | -----------
members | [Player[]](#player) | The team members
owner | [Player](#player) | A summary of the owner
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
teamId | string | The Id of the team
teamName | string | The team name
teamType | string | The team type
teams | [Team[]](#team) | A JSON array of teams.

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### Team

A nested object that represents the team.

Parameter | Type | Description
--------- | ---- | -----------
members | [Player[]](#player) | The team members
owner | [Player](#player) | A summary of the owner
teamId | string | The Id of the team
teamName | string | The team name
teamType | string | The team type

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
teamId&#124;teamType | REQUIRED | Both teamId and teamType have not been provided
team | INVALID | The teamId or the teamType do not match an existing team
teamType&&ownerId | NOT_UNIQUE | The ownerId / teamType combination has multiple teams related to it

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GetTeamRequest()
		.SetAnalyticsData(analyticsData)
		.SetOwnerId(ownerId)
		.SetTeamId(teamId)
		.SetTeamType(teamType)
		.Send((response) => {
		GSEnumerable<var> members = response.Members; 
		var owner = response.Owner; 
		GSData scriptData = response.ScriptData; 
		string teamId = response.TeamId; 
		string teamName = response.TeamName; 
		string teamType = response.TeamType; 
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
	    .createGetTeamRequest()
		.setAnalyticsData(analyticsData)
		.setOwnerId(ownerId)
		.setTeamId(teamId)
		.setTeamType(teamType)
		.send(function(response:com.gamesparks.api.responses.GetTeamResponse):void {
		var members:Vector.<Player> = response.getMembers(); 
		var owner:Player = response.getOwner(); 
		var scriptData:ScriptData = response.getScriptData(); 
		var teamId:String = response.getTeamId(); 
		var teamName:String = response.getTeamName(); 
		var teamType:String = response.getTeamType(); 
		var teams:Vector.<Team> = response.getTeams(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetTeamRequest* request = [[GSGetTeamRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setOwnerId:ownerId;
	[request setTeamId:teamId;
	[request setTeamType:teamType;
	[request setCallback:^ (GSGetTeamResponse* response) {
	NSArray* members = [response getMembers]; 
	GSPlayer* owner = [response getOwner]; 
	NSDictionary* scriptData = [response getScriptData]; 
	NSString* teamId = [response getTeamId]; 
	NSString* teamName = [response getTeamName]; 
	NSString* teamType = [response getTeamType]; 
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
	
	void GetTeamRequest_Response(GS& gsInstance, const GetTeamResponse& response) {
	gsstl:vector<Types::Player*> members = response.getMembers(); 
	Types::Player* owner = response.getOwner(); 
	GSData scriptData = response.getScriptData(); 
	gsstl::string teamId = response.getTeamId(); 
	gsstl::string teamName = response.getTeamName(); 
	gsstl::string teamType = response.getTeamType(); 
	gsstl:vector<Types::Team*> teams = response.getTeams(); 
	}
	......
	
	GetTeamRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetOwnerId(ownerId)
	request.SetTeamId(teamId)
	request.SetTeamType(teamType)
	request.Send(GetTeamRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetTeamRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetTeamResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetTeamRequest()
	.setAnalyticsData(analyticsData)
	.setOwnerId(ownerId)
	.setTeamId(teamId)
	.setTeamType(teamType)
	.send(new GSEventListener<GetTeamResponse>() {
		@Override
		public void onEvent(GetTeamResponse response) {
			List<Player> members = response.getMembers(); 
			Player owner = response.getOwner(); 
			GSData scriptData = response.getScriptData(); 
			String teamId = response.getTeamId(); 
			String teamName = response.getTeamName(); 
			String teamType = response.getTeamType(); 
			List<Team> teams = response.getTeams(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetTeamRequest();
	request.analyticsData = ...;
	request.ownerId = ...;
	request.teamId = ...;
	request.teamType = ...;
	var response = request.Send();
	
var members = response.members; 
var owner = response.owner; 
var scriptData = response.scriptData; 
var teamId = response.teamId; 
var teamName = response.teamName; 
var teamType = response.teamType; 
var teams = response.teams; 
```


