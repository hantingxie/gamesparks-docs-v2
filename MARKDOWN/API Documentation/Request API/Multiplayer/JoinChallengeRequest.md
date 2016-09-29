
# JoinChallengeRequest


Allows a player to join an open challenge.


<a href="https://api.gamesparks.net/#joinchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
challengeInstanceId | Yes | string | The ID of the challenge
eligibility | Yes | JSON | Optional.  Allows the current player's eligibility to be overridden by what is provided here.
message | No | string | An optional message to send with the challenge

## Response Parameters


A response to a player joining a challenge

Parameter | Type | Description
--------- | ---- | -----------
joined | boolean | Whether the player successfully joined the challenge
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
challengeInstanceId | UNKNOWN | No challenge could be found with the given challengeInstanceId
JOIN | NOT_FRIEND | The player is trying to join a FRIENDS challenge that is owned by someone with whom they are not a friend
JOIN | Must be a PUBLIC|FRIENDS challenge to join | The player is trying to join a PRIVATE challenge, should use AcceptChallengeRequest instead
eligibility | { "XXX" : "UNRECOGNISED"} | XXX is not a valid field of eligibility
eligibility | { "segments" : {"XXX" : "MALFORMED"}} | The value provied for XXX is not in the correct format
eligibility | { "missingSegments" : {"XXX" : ["YYY", "ZZZ"]}} | To join this challenge the player must have segment XXX with value YYY or ZZZ
eligibility | { "invalidSegments" :  { "actual" : {"XXX" : "YYY"}, "required" : {"XXX" : "ZZZ"}} | This player has segment XXX value YYY however this challenge requires a segment XXX value of ZZZ

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new JoinChallengeRequest()
		.SetAnalyticsData(analyticsData)
		.SetChallengeInstanceId(challengeInstanceId)
		.SetEligibility(eligibility)
		.SetMessage(message)
		.Send((response) => {
		bool? joined = response.Joined; 
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
	    .createJoinChallengeRequest()
		.setAnalyticsData(analyticsData)
		.setChallengeInstanceId(challengeInstanceId)
		.setEligibility(eligibility)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.JoinChallengeResponse):void {
		var joined:Boolean = response.getJoined(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSJoinChallengeRequest* request = [[GSJoinChallengeRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setChallengeInstanceId:challengeInstanceId;
	[request setEligibility:eligibility;
	[request setMessage:message;
	[request setCallback:^ (GSJoinChallengeResponse* response) {
	BOOL joined = [response getJoined]; 
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
	
	void JoinChallengeRequest_Response(GS& gsInstance, const JoinChallengeResponse& response) {
	Optional::t_BoolOptional joined = response.getJoined(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	JoinChallengeRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetEligibility(eligibility)
	request.SetMessage(message)
	request.Send(JoinChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.JoinChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.JoinChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createJoinChallengeRequest()
	.setAnalyticsData(analyticsData)
	.setChallengeInstanceId(challengeInstanceId)
	.setEligibility(eligibility)
	.setMessage(message)
	.send(new GSEventListener<JoinChallengeResponse>() {
		@Override
		public void onEvent(JoinChallengeResponse response) {
			Boolean joined = response.getJoined(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.JoinChallengeRequest();
	request.analyticsData = ...;
	request.challengeInstanceId = ...;
	request.eligibility = ...;
	request.message = ...;
	var response = request.Send();
	
var joined = response.joined; 
var scriptData = response.scriptData; 
```


