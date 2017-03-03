
# AcceptChallengeRequest


Accepts a challenge that has been issued to the current player.


<a href="https://api.gamesparks.net/#acceptchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challengeInstanceId | Yes | string | The ID of the challenge
message | No | string | An optional message to send with the challenge

## Response Parameters


A response containing the challenge instance id that was accepted.

Parameter | Type | Description
--------- | ---- | -----------
challengeInstanceId | string | The ID of the challenge
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
challengeInstanceId | INVALID | The ID does not match a challenge the user is involved with

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new AcceptChallengeRequest()
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
	    .createAcceptChallengeRequest()
		.setChallengeInstanceId(challengeInstanceId)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.AcceptChallengeResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSAcceptChallengeRequest* request = [[GSAcceptChallengeRequest alloc] init];
	[request setChallengeInstanceId:challengeInstanceId;
	[request setMessage:message;
	[request setCallback:^ (GSAcceptChallengeResponse* response) {
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
	
	void AcceptChallengeRequest_Response(GS& gsInstance, const AcceptChallengeResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	AcceptChallengeRequest request(gsInstance);
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetMessage(message)
	request.Send(AcceptChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.AcceptChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AcceptChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createAcceptChallengeRequest()
	.setChallengeInstanceId(challengeInstanceId)
	.setMessage(message)
	.send(new GSEventListener<AcceptChallengeResponse>() {
		@Override
		public void onEvent(AcceptChallengeResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.AcceptChallengeRequest();
	request.challengeInstanceId = ...;
	request.message = ...;
	var response = request.Send();
	
var challengeInstanceId = response.challengeInstanceId; 
var scriptData = response.scriptData; 
```


