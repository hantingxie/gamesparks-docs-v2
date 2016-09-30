---
src: /API Documentation/Request API/Multiplayer/LogChallengeEventRequest.md
---

# LogChallengeEventRequest


Allows a user defined event to be triggered. The event will be posted to the challenge specified.

This call differs from most as it does not have a fixed format. The @class, challengeInstanceId and eventKey attributes are common, but the rest of the attributes are as defined in the Event object configured in the dev portal.

The example below shows a request to en event with a short code of HS with 2 attributes, 'HS' & 'GL'.


<a href="https://api.gamesparks.net/#logchallengeeventrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
challengeInstanceId | Yes | string | The ID challenge instance to target
eventKey | Yes | string | The short code of the event to trigger

## Response Parameters


A response to a log challenge event request 

Parameter | Type | Description
--------- | ---- | -----------
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
challengeInstanceId | INVALID | The challengeInstanceId does not match a challenge the user has access to
[attribute short code]	 | REQUIRED | Each attribute defined in the event must be supplied.

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new LogChallengeEventRequest()
		.SetAnalyticsData(analyticsData)
		.SetChallengeInstanceId(challengeInstanceId)
		.SetEventKey(eventKey)
		.Send((response) => {
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
	    .createLogChallengeEventRequest()
		.setAnalyticsData(analyticsData)
		.setChallengeInstanceId(challengeInstanceId)
		.setEventKey(eventKey)
		.send(function(response:com.gamesparks.api.responses.LogChallengeEventResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSLogChallengeEventRequest* request = [[GSLogChallengeEventRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setChallengeInstanceId:challengeInstanceId;
	[request setEventKey:eventKey;
	[request setCallback:^ (GSLogChallengeEventResponse* response) {
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
	
	void LogChallengeEventRequest_Response(GS& gsInstance, const LogChallengeEventResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	LogChallengeEventRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetEventKey(eventKey)
	request.Send(LogChallengeEventRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.LogChallengeEventRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.LogChallengeEventResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createLogChallengeEventRequest()
	.setAnalyticsData(analyticsData)
	.setChallengeInstanceId(challengeInstanceId)
	.setEventKey(eventKey)
	.send(new GSEventListener<LogChallengeEventResponse>() {
		@Override
		public void onEvent(LogChallengeEventResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.LogChallengeEventRequest();
	request.analyticsData = ...;
	request.challengeInstanceId = ...;
	request.eventKey = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


