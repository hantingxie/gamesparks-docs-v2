---
src: /API Documentation/Request API/Player/GetMessageRequest.md
---

# GetMessageRequest


Returns the full details of a message.


<a href="https://api.gamesparks.net/#getmessagerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
messageId | Yes | string | The messageId of the message retreive

## Response Parameters


A response containing the message data for a given message

Parameter | Type | Description
--------- | ---- | -----------
message | JSON | The message data
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
	new GetMessageRequest()
		.SetAnalyticsData(analyticsData)
		.SetMessageId(messageId)
		.Send((response) => {
		GSData message = response.Message; 
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
	    .createGetMessageRequest()
		.setAnalyticsData(analyticsData)
		.setMessageId(messageId)
		.send(function(response:com.gamesparks.api.responses.GetMessageResponse):void {
		var message:Object = response.getMessage(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetMessageRequest* request = [[GSGetMessageRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setMessageId:messageId;
	[request setCallback:^ (GSGetMessageResponse* response) {
	NSDictionary* message = [response getMessage]; 
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
	
	void GetMessageRequest_Response(GS& gsInstance, const GetMessageResponse& response) {
	GSData message = response.getMessage(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	GetMessageRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetMessageId(messageId)
	request.Send(GetMessageRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetMessageRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetMessageResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetMessageRequest()
	.setAnalyticsData(analyticsData)
	.setMessageId(messageId)
	.send(new GSEventListener<GetMessageResponse>() {
		@Override
		public void onEvent(GetMessageResponse response) {
			GSData message = response.getMessage(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetMessageRequest();
	request.analyticsData = ...;
	request.messageId = ...;
	var response = request.Send();
	
var message = response.message; 
var scriptData = response.scriptData; 
```


