---
src: /API Documentation/Request API/Multiplayer/FindMatchRequest.md
---

# FindMatchRequest


@Deprecated. Use MatchmakingRequest instead.

Find a match for this player, using the given skill and matchShortCode.

Players looking for a match using the same matchShortCode will be considered for a match, based on the matchConfig.

Each player must match the other for the match to be found.


<a href="https://api.gamesparks.net/#findmatchrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
action | No | string | The action to take on the already in-flight request for this match. Currently supported actions are: 'cancel'
matchGroup | No | string | Optional. Players will be grouped based on the distinct value passed in here, only players in the same group can be matched together
matchShortCode | Yes | string | The shortCode of the match type this player is registering for
skill | No | number | The skill of the player looking for a match

## Response Parameters


A response to a find match request

Parameter | Type | Description
--------- | ---- | -----------
accessToken | string | The accessToken used to authenticate this player for this match
host | string | The host to connect to for this match
matchData | JSON | MatchData is arbitrary data that can be stored in a Match instance by a Cloud Code script.
matchId | string | The id for this match instance
opponents | [Player[]](#player) | The opponents this player has been matched against
peerId | number | The peerId of this player within the match
playerId | string | The id of the current player
port | number | The port to connect to for this match
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

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
match | NOT_FOUND | No match was found for the current player
match | HEAD_TO_HEAD_ONLY | To match multiple opponents please use MatchmakingRequest
match | NO_DROP_IN_DROP_OUT_AVAILABLE | To use the drop-in-drop-out functionality please use MatchmakingRequest
match | NO_MANUAL_MATCHMAKING | To use the manual matchmaking functionality please use MatchmakingRequest

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new FindMatchRequest()
		.SetAction(action)
		.SetMatchGroup(matchGroup)
		.SetMatchShortCode(matchShortCode)
		.SetSkill(skill)
		.Send((response) => {
		string accessToken = response.AccessToken; 
		string host = response.Host; 
		GSData matchData = response.MatchData; 
		string matchId = response.MatchId; 
		GSEnumerable<var> opponents = response.Opponents; 
		int? peerId = response.PeerId; 
		string playerId = response.PlayerId; 
		int? port = response.Port; 
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
	    .createFindMatchRequest()
		.setAction(action)
		.setMatchGroup(matchGroup)
		.setMatchShortCode(matchShortCode)
		.setSkill(skill)
		.send(function(response:com.gamesparks.api.responses.FindMatchResponse):void {
		var accessToken:String = response.getAccessToken(); 
		var host:String = response.getHost(); 
		var matchData:Object = response.getMatchData(); 
		var matchId:String = response.getMatchId(); 
		var opponents:Vector.<Player> = response.getOpponents(); 
		var peerId:Number = response.getPeerId(); 
		var playerId:String = response.getPlayerId(); 
		var port:Number = response.getPort(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSFindMatchRequest* request = [[GSFindMatchRequest alloc] init];
	[request setAction:action;
	[request setMatchGroup:matchGroup;
	[request setMatchShortCode:matchShortCode;
	[request setSkill:skill;
	[request setCallback:^ (GSFindMatchResponse* response) {
	NSString* accessToken = [response getAccessToken]; 
	NSString* host = [response getHost]; 
	NSDictionary* matchData = [response getMatchData]; 
	NSString* matchId = [response getMatchId]; 
	NSArray* opponents = [response getOpponents]; 
	NSNumber* peerId = [response getPeerId]; 
	NSString* playerId = [response getPlayerId]; 
	NSNumber* port = [response getPort]; 
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
	
	void FindMatchRequest_Response(GS& gsInstance, const FindMatchResponse& response) {
	gsstl::string accessToken = response.getAccessToken(); 
	gsstl::string host = response.getHost(); 
	GSData matchData = response.getMatchData(); 
	gsstl::string matchId = response.getMatchId(); 
	gsstl:vector<Types::Player*> opponents = response.getOpponents(); 
	Optional::t_LongOptional peerId = response.getPeerId(); 
	gsstl::string playerId = response.getPlayerId(); 
	Optional::t_LongOptional port = response.getPort(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	FindMatchRequest request(gsInstance);
	request.SetAction(action)
	request.SetMatchGroup(matchGroup)
	request.SetMatchShortCode(matchShortCode)
	request.SetSkill(skill)
	request.Send(FindMatchRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.FindMatchRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.FindMatchResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createFindMatchRequest()
	.setAction(action)
	.setMatchGroup(matchGroup)
	.setMatchShortCode(matchShortCode)
	.setSkill(skill)
	.send(new GSEventListener<FindMatchResponse>() {
		@Override
		public void onEvent(FindMatchResponse response) {
			String accessToken = response.getAccessToken(); 
			String host = response.getHost(); 
			GSData matchData = response.getMatchData(); 
			String matchId = response.getMatchId(); 
			List<Player> opponents = response.getOpponents(); 
			Integer peerId = response.getPeerId(); 
			String playerId = response.getPlayerId(); 
			Integer port = response.getPort(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.FindMatchRequest();
	request.action = ...;
	request.matchGroup = ...;
	request.matchShortCode = ...;
	request.skill = ...;
	var response = request.Send();
	
var accessToken = response.accessToken; 
var host = response.host; 
var matchData = response.matchData; 
var matchId = response.matchId; 
var opponents = response.opponents; 
var peerId = response.peerId; 
var playerId = response.playerId; 
var port = response.port; 
var scriptData = response.scriptData; 
```


