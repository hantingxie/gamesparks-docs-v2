---
src: /API Documentation/Request API/Teams/LeaveTeamRequest.md
---

# LeaveTeamRequest


Allows a player to leave a team.


<a href="https://api.gamesparks.net/#leaveteamrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
ownerId | No | string | The team owner to find, used in combination with teamType. If not supplied the current players id will be used
teamId | No | string | The teamId to find (may be null if teamType supplied)
teamType | No | string | The teamType to find, used in combination with the current player, or the player defined by ownerId

## Response Parameters


A response to a player leaving a team

Parameter | Type | Description
--------- | ---- | -----------
members | [Player[]](#player) | The team members
owner | [Player](#player) | A summary of the owner
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
teamId | string | The Id of the team
teamName | string | The team name
teamType | string | The team type

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

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
teamId&#124;teamType | REQUIRED | Both teamId and teamType have not been provided
team | INVALID | The teamId or the teamType do not match an existing team
team | CANNOT_LEAVE_OWNED_TEAM | The current player is trying to leave a team they own.
team | NOT_MEMBER | The current player is not a mamber of the team they are requesting to leave
teamType&&ownerId | NOT_UNIQUE | The ownerId / teamType combination has multiple teams related to it

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new LeaveTeamRequest()
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
	    .createLeaveTeamRequest()
		.setAnalyticsData(analyticsData)
		.setOwnerId(ownerId)
		.setTeamId(teamId)
		.setTeamType(teamType)
		.send(function(response:com.gamesparks.api.responses.LeaveTeamResponse):void {
		var members:Vector.<Player> = response.getMembers(); 
		var owner:Player = response.getOwner(); 
		var scriptData:ScriptData = response.getScriptData(); 
		var teamId:String = response.getTeamId(); 
		var teamName:String = response.getTeamName(); 
		var teamType:String = response.getTeamType(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSLeaveTeamRequest* request = [[GSLeaveTeamRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setOwnerId:ownerId;
	[request setTeamId:teamId;
	[request setTeamType:teamType;
	[request setCallback:^ (GSLeaveTeamResponse* response) {
	NSArray* members = [response getMembers]; 
	GSPlayer* owner = [response getOwner]; 
	NSDictionary* scriptData = [response getScriptData]; 
	NSString* teamId = [response getTeamId]; 
	NSString* teamName = [response getTeamName]; 
	NSString* teamType = [response getTeamType]; 
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
	
	void LeaveTeamRequest_Response(GS& gsInstance, const LeaveTeamResponse& response) {
	gsstl:vector<Types::Player*> members = response.getMembers(); 
	Types::Player* owner = response.getOwner(); 
	GSData scriptData = response.getScriptData(); 
	gsstl::string teamId = response.getTeamId(); 
	gsstl::string teamName = response.getTeamName(); 
	gsstl::string teamType = response.getTeamType(); 
	}
	......
	
	LeaveTeamRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetOwnerId(ownerId)
	request.SetTeamId(teamId)
	request.SetTeamType(teamType)
	request.Send(LeaveTeamRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.LeaveTeamRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.LeaveTeamResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createLeaveTeamRequest()
	.setAnalyticsData(analyticsData)
	.setOwnerId(ownerId)
	.setTeamId(teamId)
	.setTeamType(teamType)
	.send(new GSEventListener<LeaveTeamResponse>() {
		@Override
		public void onEvent(LeaveTeamResponse response) {
			List<Player> members = response.getMembers(); 
			Player owner = response.getOwner(); 
			GSData scriptData = response.getScriptData(); 
			String teamId = response.getTeamId(); 
			String teamName = response.getTeamName(); 
			String teamType = response.getTeamType(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.LeaveTeamRequest();
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
```


