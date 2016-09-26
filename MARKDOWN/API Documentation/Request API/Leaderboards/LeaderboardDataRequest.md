---
src: /API Documentation/Request API/Leaderboards/LeaderboardDataRequest.md
---

# LeaderboardDataRequest


Returns the top data for either the specified global leaderboard or the specified challenges leaderboard. The data is sorted as defined in the rules specified in the leaderboard configuration.

The response contains the top of the leaderboard, and returns the number of entries as defined in the entryCount parameter.

If a shortCode is supplied, the response will contain the global leaderboard data. If a challengeInstanceId is supplied, the response will contain the leaderboard data for the challenge.


<a href="https://api.gamesparks.net/#leaderboarddatarequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challengeInstanceId | No | string | The challenge instance to get the leaderboard data for
dontErrorOnNotSocial | No | boolean | The default behaviour on a social request is to error if the player has no friends (NOTSOCIAL).  Set this flag to suppress that error and return the player's leaderboard entry instead.
entryCount | Yes | number | The number of items to return in a page (default=50)
friendIds | No | string[] | A friend id or an array of friend ids to use instead of the player's social friends
includeFirst | No | number | Number of entries to include from head of the list
includeLast | No | number | Number of entries to include from tail of the list
inverseSocial | No | boolean | Returns the leaderboard excluding the player's social friends
leaderboardShortCode | No | string | The short code of the leaderboard
offset | No | number | The offset into the set of leaderboards returned
social | No | boolean | If True returns a leaderboard of the player's social friends
teamIds | No | string[] | The IDs of the teams you are interested in
teamTypes | No | string[] | The type of team you are interested in

## Response Parameters


A response containing leaderboard data

Parameter | Type | Description
--------- | ---- | -----------
challengeInstanceId | string | The leaderboard's challenge id
data | [LeaderboardData[]](#leaderboarddata) | The leaderboard data
first | [LeaderboardData[]](#leaderboarddata) | The first item in the leaderboard data
last | [LeaderboardData[]](#leaderboarddata) | The last item in the leaderboard data
leaderboardShortCode | string | The leaderboard short code
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### LeaderboardData

Leaderboard entry data

As well as the parameters below there may be others depending on your game's configuration.

Parameter | Type | Description
--------- | ---- | -----------
city | string | The city where the player was located when they logged this leaderboard entry.
country | string | The country code where the player was located when they logged this leaderboard entry.
externalIds | JSON | The players rank.
rank | number | The players rank.
userId | string | The unique player id for this leaderboard entry.
userName | string | The players display name.
when | string | The date when this leaderboard entry was created.

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
leaderboardShortCode&#124;challengeInstanceId | ONLY_ONE | Both shortCode and challengeInstanceId were supplied, only one should be supplied
leaderboardShortCode&#124;challengeInstanceId | REQUIRED | Both shortCode and challengeInstanceId were missing
leaderboardShortCode | INVALID | The shortCode does not match a configured leaderboard
currentUser | NOTSOCIAL | The current player does not have any game friends
challengeInstanceId	 | NO_LEADERBOARD | The challengeInstanceId maps to a challenge without a leaderboard configured
challengeInstanceId	 | INVALID | The challengeInstanceId supplied did not match a challenge related to the current play

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new LeaderboardDataRequest()
		.SetChallengeInstanceId(challengeInstanceId)
		.SetDontErrorOnNotSocial(dontErrorOnNotSocial)
		.SetEntryCount(entryCount)
		.SetFriendIds(friendIds)
		.SetIncludeFirst(includeFirst)
		.SetIncludeLast(includeLast)
		.SetInverseSocial(inverseSocial)
		.SetLeaderboardShortCode(leaderboardShortCode)
		.SetOffset(offset)
		.SetSocial(social)
		.SetTeamIds(teamIds)
		.SetTeamTypes(teamTypes)
		.Send((response) => {
		string challengeInstanceId = response.ChallengeInstanceId; 
		GSEnumerable<var> data = response.Data; 
		GSEnumerable<var> first = response.First; 
		GSEnumerable<var> last = response.Last; 
		string leaderboardShortCode = response.LeaderboardShortCode; 
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
	    .createLeaderboardDataRequest()
		.setChallengeInstanceId(challengeInstanceId)
		.setDontErrorOnNotSocial(dontErrorOnNotSocial)
		.setEntryCount(entryCount)
		.setFriendIds(friendIds)
		.setIncludeFirst(includeFirst)
		.setIncludeLast(includeLast)
		.setInverseSocial(inverseSocial)
		.setLeaderboardShortCode(leaderboardShortCode)
		.setOffset(offset)
		.setSocial(social)
		.setTeamIds(teamIds)
		.setTeamTypes(teamTypes)
		.send(function(response:com.gamesparks.api.responses.LeaderboardDataResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var data:Vector.<LeaderboardData> = response.getData(); 
		var first:Vector.<LeaderboardData> = response.getFirst(); 
		var last:Vector.<LeaderboardData> = response.getLast(); 
		var leaderboardShortCode:String = response.getLeaderboardShortCode(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSLeaderboardDataRequest* request = [[GSLeaderboardDataRequest alloc] init];
	[request setChallengeInstanceId:challengeInstanceId;
	[request setDontErrorOnNotSocial:dontErrorOnNotSocial;
	[request setEntryCount:entryCount;
	[request setFriendIds:friendIds;
	[request setIncludeFirst:includeFirst;
	[request setIncludeLast:includeLast;
	[request setInverseSocial:inverseSocial;
	[request setLeaderboardShortCode:leaderboardShortCode;
	[request setOffset:offset;
	[request setSocial:social;
	[request setTeamIds:teamIds;
	[request setTeamTypes:teamTypes;
	[request setCallback:^ (GSLeaderboardDataResponse* response) {
	NSString* challengeInstanceId = [response getChallengeInstanceId]; 
	NSArray* data = [response getData]; 
	NSArray* first = [response getFirst]; 
	NSArray* last = [response getLast]; 
	NSString* leaderboardShortCode = [response getLeaderboardShortCode]; 
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
	
	void LeaderboardDataRequest_Response(GS& gsInstance, const LeaderboardDataResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	gsstl:vector<Types::LeaderboardData*> data = response.getData(); 
	gsstl:vector<Types::LeaderboardData*> first = response.getFirst(); 
	gsstl:vector<Types::LeaderboardData*> last = response.getLast(); 
	gsstl::string leaderboardShortCode = response.getLeaderboardShortCode(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	LeaderboardDataRequest request(gsInstance);
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetDontErrorOnNotSocial(dontErrorOnNotSocial)
	request.SetEntryCount(entryCount)
	request.SetFriendIds(friendIds)
	request.SetIncludeFirst(includeFirst)
	request.SetIncludeLast(includeLast)
	request.SetInverseSocial(inverseSocial)
	request.SetLeaderboardShortCode(leaderboardShortCode)
	request.SetOffset(offset)
	request.SetSocial(social)
	request.SetTeamIds(teamIds)
	request.SetTeamTypes(teamTypes)
	request.Send(LeaderboardDataRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.LeaderboardDataRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.LeaderboardDataResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createLeaderboardDataRequest()
	.setChallengeInstanceId(challengeInstanceId)
	.setDontErrorOnNotSocial(dontErrorOnNotSocial)
	.setEntryCount(entryCount)
	.setFriendIds(friendIds)
	.setIncludeFirst(includeFirst)
	.setIncludeLast(includeLast)
	.setInverseSocial(inverseSocial)
	.setLeaderboardShortCode(leaderboardShortCode)
	.setOffset(offset)
	.setSocial(social)
	.setTeamIds(teamIds)
	.setTeamTypes(teamTypes)
	.send(new GSEventListener<LeaderboardDataResponse>() {
		@Override
		public void onEvent(LeaderboardDataResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			List<LeaderboardData> data = response.getData(); 
			List<LeaderboardData> first = response.getFirst(); 
			List<LeaderboardData> last = response.getLast(); 
			String leaderboardShortCode = response.getLeaderboardShortCode(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.LeaderboardDataRequest();
	request.challengeInstanceId = ...;
	request.dontErrorOnNotSocial = ...;
	request.entryCount = ...;
	request.friendIds = ...;
	request.includeFirst = ...;
	request.includeLast = ...;
	request.inverseSocial = ...;
	request.leaderboardShortCode = ...;
	request.offset = ...;
	request.social = ...;
	request.teamIds = ...;
	request.teamTypes = ...;
	var response = request.Send();
	
var challengeInstanceId = response.challengeInstanceId; 
var data = response.data; 
var first = response.first; 
var last = response.last; 
var leaderboardShortCode = response.leaderboardShortCode; 
var scriptData = response.scriptData; 
```


