---
src: /API Documentation/Request API/Multiplayer/WithdrawChallengeRequest.md
---

# WithdrawChallengeRequest


Withdraws a challenge previously issued by the current player.

This can only be done while the challenge is in the ISSUED state. Once it's been accepted the challenge can not be withdrawn.


<a href="https://api.gamesparks.net/#withdrawchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challengeInstanceId | Yes | string | The ID of the challenge
message | No | string | An optional message to send with the challenge

## Response Parameters


A response containing the challenge instance id that was withdrawn by a player

Parameter | Type | Description
--------- | ---- | -----------
challengeInstanceId | string | A challenge instance id
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
challengeInstanceId | INVALID | The ID does not match a challenge in the ISSUED state that was issued by the current player

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new WithdrawChallengeRequest()
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
	    .createWithdrawChallengeRequest()
		.setChallengeInstanceId(challengeInstanceId)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.WithdrawChallengeResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSWithdrawChallengeRequest* request = [[GSWithdrawChallengeRequest alloc] init];
	[request setChallengeInstanceId:challengeInstanceId;
	[request setMessage:message;
	[request setCallback:^ (GSWithdrawChallengeResponse* response) {
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
	
	void WithdrawChallengeRequest_Response(GS& gsInstance, const WithdrawChallengeResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	WithdrawChallengeRequest request(gsInstance);
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetMessage(message)
	request.Send(WithdrawChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.WithdrawChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.WithdrawChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createWithdrawChallengeRequest()
	.setChallengeInstanceId(challengeInstanceId)
	.setMessage(message)
	.send(new GSEventListener<WithdrawChallengeResponse>() {
		@Override
		public void onEvent(WithdrawChallengeResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.WithdrawChallengeRequest();
	request.challengeInstanceId = ...;
	request.message = ...;
	var response = request.Send();
	
var challengeInstanceId = response.challengeInstanceId; 
var scriptData = response.scriptData; 
```


