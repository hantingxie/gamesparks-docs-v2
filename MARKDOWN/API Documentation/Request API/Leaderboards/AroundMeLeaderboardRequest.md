
# AroundMeLeaderboardRequest


Returns leaderboard data that is adjacent to the currently signed in player's position within the given leaderboard.


<a href="https://api.gamesparks.net/#aroundmeleaderboardrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
challengeInstanceId | No | string | The challenge instance to get the leaderboard data for
customIdFilter | No | JSON | An optional filter on the customIds.
dontErrorOnNotSocial | No | boolean | The default behaviour on a social request is to error if the player has no friends (NOTSOCIAL).  Set this flag to suppress that error and return the player's leaderboard entry instead.
entryCount | Yes | number | The number of items to return in a page (default=50)
friendIds | No | string[] | A friend id or an array of friend ids to use instead of the player's social friends
includeFirst | No | number | Number of entries to include from head of the list
includeLast | No | number | Number of entries to include from tail of the list
inverseSocial | No | boolean | Returns the leaderboard excluding the player's social friends
leaderboardShortCode | No | string | The short code of the leaderboard
social | No | boolean | If True returns a leaderboard of the player's social friends
teamIds | No | string[] | The IDs of the teams you are interested in
teamTypes | No | string[] | The type of team you are interested in

## Response Parameters


A response containing leaderboard data around the current player

Parameter | Type | Description
--------- | ---- | -----------
challengeInstanceId | string | The leaderboard's challenge id
data | [LeaderboardData[]](#leaderboarddata) | The leaderboard data
first | [LeaderboardData[]](#leaderboarddata) | The first item in the leaderboard data
last | [LeaderboardData[]](#leaderboarddata) | The last item in the leaderboard data
leaderboardShortCode | string | The leaderboard short code
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
social | boolean | True if the response contains a social leaderboard's data

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
challengeInstanceId | NO_LEADERBOARD | The challengeInstanceId maps to a challenge without a leaderboard configured
challengeInstanceId | INVALID | The challengeInstanceId supplied did not match a challenge related to the current play
challengeInstanceVersion | INVALID | The challengeInstance predates support for this request type

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new AroundMeLeaderboardRequest()
		.SetAnalyticsData(analyticsData)
		.SetChallengeInstanceId(challengeInstanceId)
		.SetCustomIdFilter(customIdFilter)
		.SetDontErrorOnNotSocial(dontErrorOnNotSocial)
		.SetEntryCount(entryCount)
		.SetFriendIds(friendIds)
		.SetIncludeFirst(includeFirst)
		.SetIncludeLast(includeLast)
		.SetInverseSocial(inverseSocial)
		.SetLeaderboardShortCode(leaderboardShortCode)
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
		bool? social = response.Social; 
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
	    .createAroundMeLeaderboardRequest()
		.setAnalyticsData(analyticsData)
		.setChallengeInstanceId(challengeInstanceId)
		.setCustomIdFilter(customIdFilter)
		.setDontErrorOnNotSocial(dontErrorOnNotSocial)
		.setEntryCount(entryCount)
		.setFriendIds(friendIds)
		.setIncludeFirst(includeFirst)
		.setIncludeLast(includeLast)
		.setInverseSocial(inverseSocial)
		.setLeaderboardShortCode(leaderboardShortCode)
		.setSocial(social)
		.setTeamIds(teamIds)
		.setTeamTypes(teamTypes)
		.send(function(response:com.gamesparks.api.responses.AroundMeLeaderboardResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var data:Vector.<LeaderboardData> = response.getData(); 
		var first:Vector.<LeaderboardData> = response.getFirst(); 
		var last:Vector.<LeaderboardData> = response.getLast(); 
		var leaderboardShortCode:String = response.getLeaderboardShortCode(); 
		var scriptData:ScriptData = response.getScriptData(); 
		var social:Boolean = response.getSocial(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSAroundMeLeaderboardRequest* request = [[GSAroundMeLeaderboardRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setChallengeInstanceId:challengeInstanceId;
	[request setCustomIdFilter:customIdFilter;
	[request setDontErrorOnNotSocial:dontErrorOnNotSocial;
	[request setEntryCount:entryCount;
	[request setFriendIds:friendIds;
	[request setIncludeFirst:includeFirst;
	[request setIncludeLast:includeLast;
	[request setInverseSocial:inverseSocial;
	[request setLeaderboardShortCode:leaderboardShortCode;
	[request setSocial:social;
	[request setTeamIds:teamIds;
	[request setTeamTypes:teamTypes;
	[request setCallback:^ (GSAroundMeLeaderboardResponse* response) {
	NSString* challengeInstanceId = [response getChallengeInstanceId]; 
	NSArray* data = [response getData]; 
	NSArray* first = [response getFirst]; 
	NSArray* last = [response getLast]; 
	NSString* leaderboardShortCode = [response getLeaderboardShortCode]; 
	NSDictionary* scriptData = [response getScriptData]; 
	BOOL social = [response getSocial]; 
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
	
	void AroundMeLeaderboardRequest_Response(GS& gsInstance, const AroundMeLeaderboardResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	gsstl:vector<Types::LeaderboardData*> data = response.getData(); 
	gsstl:vector<Types::LeaderboardData*> first = response.getFirst(); 
	gsstl:vector<Types::LeaderboardData*> last = response.getLast(); 
	gsstl::string leaderboardShortCode = response.getLeaderboardShortCode(); 
	GSData scriptData = response.getScriptData(); 
	Optional::t_BoolOptional social = response.getSocial(); 
	}
	......
	
	AroundMeLeaderboardRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetCustomIdFilter(customIdFilter)
	request.SetDontErrorOnNotSocial(dontErrorOnNotSocial)
	request.SetEntryCount(entryCount)
	request.SetFriendIds(friendIds)
	request.SetIncludeFirst(includeFirst)
	request.SetIncludeLast(includeLast)
	request.SetInverseSocial(inverseSocial)
	request.SetLeaderboardShortCode(leaderboardShortCode)
	request.SetSocial(social)
	request.SetTeamIds(teamIds)
	request.SetTeamTypes(teamTypes)
	request.Send(AroundMeLeaderboardRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.AroundMeLeaderboardRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AroundMeLeaderboardResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createAroundMeLeaderboardRequest()
	.setAnalyticsData(analyticsData)
	.setChallengeInstanceId(challengeInstanceId)
	.setCustomIdFilter(customIdFilter)
	.setDontErrorOnNotSocial(dontErrorOnNotSocial)
	.setEntryCount(entryCount)
	.setFriendIds(friendIds)
	.setIncludeFirst(includeFirst)
	.setIncludeLast(includeLast)
	.setInverseSocial(inverseSocial)
	.setLeaderboardShortCode(leaderboardShortCode)
	.setSocial(social)
	.setTeamIds(teamIds)
	.setTeamTypes(teamTypes)
	.send(new GSEventListener<AroundMeLeaderboardResponse>() {
		@Override
		public void onEvent(AroundMeLeaderboardResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			List<LeaderboardData> data = response.getData(); 
			List<LeaderboardData> first = response.getFirst(); 
			List<LeaderboardData> last = response.getLast(); 
			String leaderboardShortCode = response.getLeaderboardShortCode(); 
			GSData scriptData = response.getScriptData(); 
			Boolean social = response.getSocial(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.AroundMeLeaderboardRequest();
	request.analyticsData = ...;
	request.challengeInstanceId = ...;
	request.customIdFilter = ...;
	request.dontErrorOnNotSocial = ...;
	request.entryCount = ...;
	request.friendIds = ...;
	request.includeFirst = ...;
	request.includeLast = ...;
	request.inverseSocial = ...;
	request.leaderboardShortCode = ...;
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
var social = response.social; 
```


