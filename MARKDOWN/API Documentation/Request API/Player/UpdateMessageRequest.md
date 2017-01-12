
# UpdateMessageRequest


Allows a message status to be updated.


<a href="https://api.gamesparks.net/#updatemessagerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
messageId | Yes | string | The messageId of the message to update
status | Yes | string | The status to set on the message

## Response Parameters


A response to an update message request

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
	new UpdateMessageRequest()
		.SetMessageId(messageId)
		.SetStatus(status)
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
	    .createUpdateMessageRequest()
		.setMessageId(messageId)
		.setStatus(status)
		.send(function(response:com.gamesparks.api.responses.UpdateMessageResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSUpdateMessageRequest* request = [[GSUpdateMessageRequest alloc] init];
	[request setMessageId:messageId;
	[request setStatus:status;
	[request setCallback:^ (GSUpdateMessageResponse* response) {
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
	
	void UpdateMessageRequest_Response(GS& gsInstance, const UpdateMessageResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	UpdateMessageRequest request(gsInstance);
	request.SetMessageId(messageId)
	request.SetStatus(status)
	request.Send(UpdateMessageRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.UpdateMessageRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.UpdateMessageResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createUpdateMessageRequest()
	.setMessageId(messageId)
	.setStatus(status)
	.send(new GSEventListener<UpdateMessageResponse>() {
		@Override
		public void onEvent(UpdateMessageResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.UpdateMessageRequest();
	request.messageId = ...;
	request.status = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


