
# ListMessageDetailRequest


Returns the list of the current player's messages / notifications.

The list only contains un-dismissed messages, to dismiss a message see DismissMessageRequest Read the section on Messages to see the complete list of messages and their meaning.


<a href="https://api.gamesparks.net/#listmessagedetailrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
entryCount | No | number | The number of items to return in a page (default=50)
include | No | string | An optional filter that limits the message types returned
offset | No | number | The offset (page number) to start from (default=0)
status | No | string | The status of messages to be retrieved. If omitted, messages of all statuses will be retrieved

## Response Parameters


A response containing the list of the current players messages / notifications.

Parameter | Type | Description
--------- | ---- | -----------
messageList | [PlayerMessage[]](#playermessage) | A list of JSON objects containing player messages
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### PlayerMessage

A nested object that represents a player message.

Parameter | Type | Description
--------- | ---- | -----------
id | string | The id of the message
message | JSON | The message content
seen | boolean | Whether the message has been delivered to the client
status | string | The status of the message
when | date | The date of the message

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
	new ListMessageDetailRequest()
		.SetEntryCount(entryCount)
		.SetInclude(include)
		.SetOffset(offset)
		.SetStatus(status)
		.Send((response) => {
		GSEnumerable<var> messageList = response.MessageList; 
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
	    .createListMessageDetailRequest()
		.setEntryCount(entryCount)
		.setInclude(include)
		.setOffset(offset)
		.setStatus(status)
		.send(function(response:com.gamesparks.api.responses.ListMessageDetailResponse):void {
		var messageList:Vector.<PlayerMessage> = response.getMessageList(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListMessageDetailRequest* request = [[GSListMessageDetailRequest alloc] init];
	[request setEntryCount:entryCount;
	[request setInclude:include;
	[request setOffset:offset;
	[request setStatus:status;
	[request setCallback:^ (GSListMessageDetailResponse* response) {
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
	
	void ListMessageDetailRequest_Response(GS& gsInstance, const ListMessageDetailResponse& response) {
	gsstl:vector<Types::PlayerMessage*> messageList = response.getMessageList(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListMessageDetailRequest request(gsInstance);
	request.SetEntryCount(entryCount)
	request.SetInclude(include)
	request.SetOffset(offset)
	request.SetStatus(status)
	request.Send(ListMessageDetailRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListMessageDetailRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListMessageDetailResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListMessageDetailRequest()
	.setEntryCount(entryCount)
	.setInclude(include)
	.setOffset(offset)
	.setStatus(status)
	.send(new GSEventListener<ListMessageDetailResponse>() {
		@Override
		public void onEvent(ListMessageDetailResponse response) {
			List<PlayerMessage> messageList = response.getMessageList(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListMessageDetailRequest();
	request.entryCount = ...;
	request.include = ...;
	request.offset = ...;
	request.status = ...;
	var response = request.Send();
	
var messageList = response.messageList; 
var scriptData = response.scriptData; 
```


