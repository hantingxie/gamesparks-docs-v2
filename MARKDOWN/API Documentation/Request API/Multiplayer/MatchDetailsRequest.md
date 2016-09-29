
# MatchDetailsRequest


Find the details of an existing match this player belongs to, using the matchId


<a href="https://api.gamesparks.net/#matchdetailsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
matchId | Yes | string | The matchId to find the details of
realtimeEnabled | No | boolean | Adds realtime server details if the match has been created using Cloud Code and it has not been realtime enabled

## Response Parameters


A response to a match details request

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
matchId | NOT_FOUND | No match found with given matchId for this player

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new MatchDetailsRequest()
		.SetAnalyticsData(analyticsData)
		.SetMatchId(matchId)
		.SetRealtimeEnabled(realtimeEnabled)
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
	    .createMatchDetailsRequest()
		.setAnalyticsData(analyticsData)
		.setMatchId(matchId)
		.setRealtimeEnabled(realtimeEnabled)
		.send(function(response:com.gamesparks.api.responses.MatchDetailsResponse):void {
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
	GSMatchDetailsRequest* request = [[GSMatchDetailsRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setMatchId:matchId;
	[request setRealtimeEnabled:realtimeEnabled;
	[request setCallback:^ (GSMatchDetailsResponse* response) {
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
	
	void MatchDetailsRequest_Response(GS& gsInstance, const MatchDetailsResponse& response) {
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
	
	MatchDetailsRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetMatchId(matchId)
	request.SetRealtimeEnabled(realtimeEnabled)
	request.Send(MatchDetailsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.MatchDetailsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.MatchDetailsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createMatchDetailsRequest()
	.setAnalyticsData(analyticsData)
	.setMatchId(matchId)
	.setRealtimeEnabled(realtimeEnabled)
	.send(new GSEventListener<MatchDetailsResponse>() {
		@Override
		public void onEvent(MatchDetailsResponse response) {
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

	var request = new SparkRequests.MatchDetailsRequest();
	request.analyticsData = ...;
	request.matchId = ...;
	request.realtimeEnabled = ...;
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


