
# ListMessageRequest


Returns the list of the current player's messages / notifications.

The list only contains un-dismissed messages, to dismiss a message see DismissMessageRequest Read the section on Messages to see the complete list of messages and their meaning.


<a href="https://api.gamesparks.net/#listmessagerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
entryCount | No | number | The number of items to return in a page (default=50)
include | No | string | An optional filter that limits the message types returned
offset | No | number | The offset (page number) to start from (default=0)

## Response Parameters


A response containing the list of the current players messages / notifications.

Parameter | Type | Description
--------- | ---- | -----------
messageList | JSON[] | A list of JSON objects containing player messages
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
	new ListMessageRequest()
		.SetEntryCount(entryCount)
		.SetInclude(include)
		.SetOffset(offset)
		.Send((response) => {
		IList<GSData> messageList = response.MessageList; 
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
	    .createListMessageRequest()
		.setEntryCount(entryCount)
		.setInclude(include)
		.setOffset(offset)
		.send(function(response:com.gamesparks.api.responses.ListMessageResponse):void {
		var messageList:Vector.<Object> = response.getMessageList(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListMessageRequest* request = [[GSListMessageRequest alloc] init];
	[request setEntryCount:entryCount;
	[request setInclude:include;
	[request setOffset:offset;
	[request setCallback:^ (GSListMessageResponse* response) {
	NSArray* messageList = [response getMessageList]; 
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
	
	void ListMessageRequest_Response(GS& gsInstance, const ListMessageResponse& response) {
	gsstl:vector<GSData> messageList = response.getMessageList(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListMessageRequest request(gsInstance);
	request.SetEntryCount(entryCount)
	request.SetInclude(include)
	request.SetOffset(offset)
	request.Send(ListMessageRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListMessageRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListMessageResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListMessageRequest()
	.setEntryCount(entryCount)
	.setInclude(include)
	.setOffset(offset)
	.send(new GSEventListener<ListMessageResponse>() {
		@Override
		public void onEvent(ListMessageResponse response) {
			List<GSData> messageList = response.getMessageList(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListMessageRequest();
	request.entryCount = ...;
	request.include = ...;
	request.offset = ...;
	var response = request.Send();
	
var messageList = response.messageList; 
var scriptData = response.scriptData; 
```


