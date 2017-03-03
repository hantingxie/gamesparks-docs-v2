---
src: /API Documentation/Request API/Player/DismissMultipleMessagesRequest.md
---

# DismissMultipleMessagesRequest


Allows multiple messages to be dismissed. Once dismissed the messages will no longer appear in either ListMessageResponse or ListMessageSummaryResponse.


<a href="https://api.gamesparks.net/#dismissmultiplemessagesrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
messageIds | No | string[] | The list of the messageIds to dismiss

## Response Parameters


A response to a dismiss message request

Parameter | Type | Description
--------- | ---- | -----------
failedDismissals | string[] | A list of the messageId values that were not dismissed
messagesDismissed | number | An integer describing how many messages were dismissed
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new DismissMultipleMessagesRequest()
		.SetMessageIds(messageIds)
		.Send((response) => {
		List<string> failedDismissals = response.FailedDismissals; 
		int? messagesDismissed = response.MessagesDismissed; 
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
	    .createDismissMultipleMessagesRequest()
		.setMessageIds(messageIds)
		.send(function(response:com.gamesparks.api.responses.DismissMultipleMessagesResponse):void {
		var failedDismissals:String = response.getFailedDismissals(); 
		var messagesDismissed:Number = response.getMessagesDismissed(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSDismissMultipleMessagesRequest* request = [[GSDismissMultipleMessagesRequest alloc] init];
	[request setMessageIds:messageIds;
	[request setCallback:^ (GSDismissMultipleMessagesResponse* response) {
	NSArray* failedDismissals = [response getFailedDismissals]; 
	NSNumber* messagesDismissed = [response getMessagesDismissed]; 
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
	
	void DismissMultipleMessagesRequest_Response(GS& gsInstance, const DismissMultipleMessagesResponse& response) {
	Types::String[]* failedDismissals = response.getFailedDismissals(); 
	Optional::t_LongOptional messagesDismissed = response.getMessagesDismissed(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	DismissMultipleMessagesRequest request(gsInstance);
	request.SetMessageIds(messageIds)
	request.Send(DismissMultipleMessagesRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.DismissMultipleMessagesRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.DismissMultipleMessagesResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createDismissMultipleMessagesRequest()
	.setMessageIds(messageIds)
	.send(new GSEventListener<DismissMultipleMessagesResponse>() {
		@Override
		public void onEvent(DismissMultipleMessagesResponse response) {
			List<String> failedDismissals = response.getFailedDismissals(); 
			Integer messagesDismissed = response.getMessagesDismissed(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.DismissMultipleMessagesRequest();
	request.messageIds = ...;
	var response = request.Send();
	
var failedDismissals = response.failedDismissals; 
var messagesDismissed = response.messagesDismissed; 
var scriptData = response.scriptData; 
```


