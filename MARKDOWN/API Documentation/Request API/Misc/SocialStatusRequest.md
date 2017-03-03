
# SocialStatusRequest


Returns detials of the current social connections of this player. Each connection .


<a href="https://api.gamesparks.net/#socialstatusrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A response containing the details of a the players social connections

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
statuses | [SocialStatus[]](#socialstatus) | A list of social statuses.

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### SocialStatus

A the details of a social connection

Parameter | Type | Description
--------- | ---- | -----------
active | boolean | When the token is still active.
expires | date | When the token expires (if available).
systemId | string | The identifier of the external platform.


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new SocialStatusRequest()
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
		GSEnumerable<var> statuses = response.Statuses; 
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
	    .createSocialStatusRequest()
		.send(function(response:com.gamesparks.api.responses.SocialStatusResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var statuses:Vector.<SocialStatus> = response.getStatuses(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSSocialStatusRequest* request = [[GSSocialStatusRequest alloc] init];
	[request setCallback:^ (GSSocialStatusResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
	NSArray* statuses = [response getStatuses]; 
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
	
	void SocialStatusRequest_Response(GS& gsInstance, const SocialStatusResponse& response) {
	GSData scriptData = response.getScriptData(); 
	gsstl:vector<Types::SocialStatus*> statuses = response.getStatuses(); 
	}
	......
	
	SocialStatusRequest request(gsInstance);
	request.Send(SocialStatusRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.SocialStatusRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.SocialStatusResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createSocialStatusRequest()
	.send(new GSEventListener<SocialStatusResponse>() {
		@Override
		public void onEvent(SocialStatusResponse response) {
			GSData scriptData = response.getScriptData(); 
			List<SocialStatus> statuses = response.getStatuses(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.SocialStatusRequest();
	var response = request.Send();
	
var scriptData = response.scriptData; 
var statuses = response.statuses; 
```


