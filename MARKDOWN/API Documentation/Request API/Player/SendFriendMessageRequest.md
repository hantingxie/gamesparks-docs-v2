
# SendFriendMessageRequest


Sends a message to one or more game friend(s). A game friend is someone in the players social network who also plays the game.


<a href="https://api.gamesparks.net/#sendfriendmessagerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
friendIds | Yes | string[] | One or more friend ID's. This can be supplied as a single string, or a JSON array
message | Yes | string | The message to send

## Response Parameters


A response to a send friend message request.

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
friendId | NOT_FRIEND | The friend ID passed is not linked to the current player as a game friend
friendId | INVALID | The value passed is not a valid ID

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new SendFriendMessageRequest()
		.SetAnalyticsData(analyticsData)
		.SetFriendIds(friendIds)
		.SetMessage(message)
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
	    .createSendFriendMessageRequest()
		.setAnalyticsData(analyticsData)
		.setFriendIds(friendIds)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.SendFriendMessageResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSSendFriendMessageRequest* request = [[GSSendFriendMessageRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setFriendIds:friendIds;
	[request setMessage:message;
	[request setCallback:^ (GSSendFriendMessageResponse* response) {
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
	
	void SendFriendMessageRequest_Response(GS& gsInstance, const SendFriendMessageResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	SendFriendMessageRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetFriendIds(friendIds)
	request.SetMessage(message)
	request.Send(SendFriendMessageRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.SendFriendMessageRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.SendFriendMessageResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createSendFriendMessageRequest()
	.setAnalyticsData(analyticsData)
	.setFriendIds(friendIds)
	.setMessage(message)
	.send(new GSEventListener<SendFriendMessageResponse>() {
		@Override
		public void onEvent(SendFriendMessageResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.SendFriendMessageRequest();
	request.analyticsData = ...;
	request.friendIds = ...;
	request.message = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


