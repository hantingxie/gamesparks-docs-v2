---
src: /API Documentation/Request API/Teams/CreateTeamRequest.md
---

# CreateTeamRequest


Allows a new team to be created.


<a href="https://api.gamesparks.net/#createteamrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
teamId | No | string | An optional teamId to use
teamName | Yes | string | A display name to use
teamType | Yes | string | The type of team to be created

## Response Parameters


A response containing the details of the team that was created

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
teamType | INVALID | The team type short code supplied does not exist
teamType | MAX_OWNED_REACHED | The current player has reached the ownership limit of the supplied teamType
teamType | MAX_TEAMS_REACHED | The current player has reached the membership limit of the supplied teamType
teamId | NOT_UNIQUE | The teamId supplied already exists

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new CreateTeamRequest()
		.SetTeamId(teamId)
		.SetTeamName(teamName)
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
	    .createCreateTeamRequest()
		.setTeamId(teamId)
		.setTeamName(teamName)
		.setTeamType(teamType)
		.send(function(response:com.gamesparks.api.responses.CreateTeamResponse):void {
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
	GSCreateTeamRequest* request = [[GSCreateTeamRequest alloc] init];
	[request setTeamId:teamId;
	[request setTeamName:teamName;
	[request setTeamType:teamType;
	[request setCallback:^ (GSCreateTeamResponse* response) {
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
	
	void CreateTeamRequest_Response(GS& gsInstance, const CreateTeamResponse& response) {
	gsstl:vector<Types::Player*> members = response.getMembers(); 
	Types::Player* owner = response.getOwner(); 
	GSData scriptData = response.getScriptData(); 
	gsstl::string teamId = response.getTeamId(); 
	gsstl::string teamName = response.getTeamName(); 
	gsstl::string teamType = response.getTeamType(); 
	}
	......
	
	CreateTeamRequest request(gsInstance);
	request.SetTeamId(teamId)
	request.SetTeamName(teamName)
	request.SetTeamType(teamType)
	request.Send(CreateTeamRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.CreateTeamRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.CreateTeamResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createCreateTeamRequest()
	.setTeamId(teamId)
	.setTeamName(teamName)
	.setTeamType(teamType)
	.send(new GSEventListener<CreateTeamResponse>() {
		@Override
		public void onEvent(CreateTeamResponse response) {
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

	var request = new SparkRequests.CreateTeamRequest();
	request.teamId = ...;
	request.teamName = ...;
	request.teamType = ...;
	var response = request.Send();
	
var members = response.members; 
var owner = response.owner; 
var scriptData = response.scriptData; 
var teamId = response.teamId; 
var teamName = response.teamName; 
var teamType = response.teamType; 
```


