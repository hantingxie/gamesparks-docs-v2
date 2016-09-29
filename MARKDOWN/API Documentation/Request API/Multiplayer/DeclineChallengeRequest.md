
# DeclineChallengeRequest


Declines a challenge that has been issued to the current player.


<a href="https://api.gamesparks.net/#declinechallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
challengeInstanceId | Yes | string | The ID of the challenge
message | No | string | An optional message to send with the challenge

## Response Parameters


A response containing the challenge instance id of the challenge that was declined

Parameter | Type | Description
--------- | ---- | -----------
challengeInstanceId | string | The challenge instance id
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
challengeInstanceId | INVALID | The ID does not match a challenge that has been issued

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new DeclineChallengeRequest()
		.SetAnalyticsData(analyticsData)
		.SetChallengeInstanceId(challengeInstanceId)
		.SetMessage(message)
		.Send((response) => {
		string challengeInstanceId = response.ChallengeInstanceId; 
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
	    .createDeclineChallengeRequest()
		.setAnalyticsData(analyticsData)
		.setChallengeInstanceId(challengeInstanceId)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.DeclineChallengeResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSDeclineChallengeRequest* request = [[GSDeclineChallengeRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setChallengeInstanceId:challengeInstanceId;
	[request setMessage:message;
	[request setCallback:^ (GSDeclineChallengeResponse* response) {
	NSString* challengeInstanceId = [response getChallengeInstanceId]; 
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
	
	void DeclineChallengeRequest_Response(GS& gsInstance, const DeclineChallengeResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	DeclineChallengeRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetMessage(message)
	request.Send(DeclineChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.DeclineChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.DeclineChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createDeclineChallengeRequest()
	.setAnalyticsData(analyticsData)
	.setChallengeInstanceId(challengeInstanceId)
	.setMessage(message)
	.send(new GSEventListener<DeclineChallengeResponse>() {
		@Override
		public void onEvent(DeclineChallengeResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.DeclineChallengeRequest();
	request.analyticsData = ...;
	request.challengeInstanceId = ...;
	request.message = ...;
	var response = request.Send();
	
var challengeInstanceId = response.challengeInstanceId; 
var scriptData = response.scriptData; 
```


