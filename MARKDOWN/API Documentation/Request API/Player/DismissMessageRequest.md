
# DismissMessageRequest


Allows a message to be dismissed. Once dismissed the message will no longer appear in either ListMessageResponse or ListMessageSummaryResponse.


<a href="https://api.gamesparks.net/#dismissmessagerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
messageId | Yes | string | The messageId of the message to dismiss

## Response Parameters


A response to a dismiss message request

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


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new DismissMessageRequest()
		.SetMessageId(messageId)
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
	    .createDismissMessageRequest()
		.setMessageId(messageId)
		.send(function(response:com.gamesparks.api.responses.DismissMessageResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSDismissMessageRequest* request = [[GSDismissMessageRequest alloc] init];
	[request setMessageId:messageId;
	[request setCallback:^ (GSDismissMessageResponse* response) {
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
	
	void DismissMessageRequest_Response(GS& gsInstance, const DismissMessageResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	DismissMessageRequest request(gsInstance);
	request.SetMessageId(messageId)
	request.Send(DismissMessageRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.DismissMessageRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.DismissMessageResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createDismissMessageRequest()
	.setMessageId(messageId)
	.send(new GSEventListener<DismissMessageResponse>() {
		@Override
		public void onEvent(DismissMessageResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.DismissMessageRequest();
	request.messageId = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


