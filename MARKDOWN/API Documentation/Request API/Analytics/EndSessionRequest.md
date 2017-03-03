---
src: /API Documentation/Request API/Analytics/EndSessionRequest.md
---

# EndSessionRequest


Records the end of the current player's active session.

The SDK will automatically create a new session ID when the application is started, this method can be useful to call when the app goes into the background to allow reporting on player session length.


<a href="https://api.gamesparks.net/#endsessionrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A response to an end session request

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
sessionDuration | number | The length of this session

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
	new EndSessionRequest()
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
		long? sessionDuration = response.SessionDuration; 
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
	    .createEndSessionRequest()
		.send(function(response:com.gamesparks.api.responses.EndSessionResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var sessionDuration:Number = response.getSessionDuration(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSEndSessionRequest* request = [[GSEndSessionRequest alloc] init];
	[request setCallback:^ (GSEndSessionResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
	NSNumber* sessionDuration = [response getSessionDuration]; 
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
	
	void EndSessionRequest_Response(GS& gsInstance, const EndSessionResponse& response) {
	GSData scriptData = response.getScriptData(); 
	Optional::t_LongOptional sessionDuration = response.getSessionDuration(); 
	}
	......
	
	EndSessionRequest request(gsInstance);
	request.Send(EndSessionRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.EndSessionRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.EndSessionResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createEndSessionRequest()
	.send(new GSEventListener<EndSessionResponse>() {
		@Override
		public void onEvent(EndSessionResponse response) {
			GSData scriptData = response.getScriptData(); 
			Long sessionDuration = response.getSessionDuration(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.EndSessionRequest();
	var response = request.Send();
	
var scriptData = response.scriptData; 
var sessionDuration = response.sessionDuration; 
```


