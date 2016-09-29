
# ChatOnChallengeRequest


Sends a message to all players involved in the challenge. The current player must be involved in the challenge for the message to be sent.

As the message is sent to all players, the current player will also see details of the message in the response. Read the section on response message aggregation for a description of this.


<a href="https://api.gamesparks.net/#chatonchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
challengeInstanceId | Yes | string | The ID of the challenge
message | No | string | An optional message to send with the challenge

## Response Parameters


A response to a chat on challenge request

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
challengeInstanceId | INVALID | The ID does not match a challenge the current player is involved with

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ChatOnChallengeRequest()
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
	    .createChatOnChallengeRequest()
		.setAnalyticsData(analyticsData)
		.setChallengeInstanceId(challengeInstanceId)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.ChatOnChallengeResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSChatOnChallengeRequest* request = [[GSChatOnChallengeRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setChallengeInstanceId:challengeInstanceId;
	[request setMessage:message;
	[request setCallback:^ (GSChatOnChallengeResponse* response) {
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
	
	void ChatOnChallengeRequest_Response(GS& gsInstance, const ChatOnChallengeResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ChatOnChallengeRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetMessage(message)
	request.Send(ChatOnChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ChatOnChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ChatOnChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createChatOnChallengeRequest()
	.setAnalyticsData(analyticsData)
	.setChallengeInstanceId(challengeInstanceId)
	.setMessage(message)
	.send(new GSEventListener<ChatOnChallengeResponse>() {
		@Override
		public void onEvent(ChatOnChallengeResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ChatOnChallengeRequest();
	request.analyticsData = ...;
	request.challengeInstanceId = ...;
	request.message = ...;
	var response = request.Send();
	
var challengeInstanceId = response.challengeInstanceId; 
var scriptData = response.scriptData; 
```


