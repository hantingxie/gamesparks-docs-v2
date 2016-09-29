
# LogEventRequest


Allows a user defined event to be triggered.

This call differs from most as it does not have a fixed format. The @class and eventKey attributes are common, but the rest of the attributes are as defined in the Event object configured in the dev portal.

The example below shows a request to an event with a short code of HS with 2 attributes, 'HS' & 'GL'.


<a href="https://api.gamesparks.net/#logeventrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
eventKey | Yes | string | The short code of the event to trigger

## Response Parameters


A response to a log event request 

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
	new LogEventRequest()
		.SetAnalyticsData(analyticsData)
		.SetEventKey(eventKey)
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
	    .createLogEventRequest()
		.setAnalyticsData(analyticsData)
		.setEventKey(eventKey)
		.send(function(response:com.gamesparks.api.responses.LogEventResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSLogEventRequest* request = [[GSLogEventRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setEventKey:eventKey;
	[request setCallback:^ (GSLogEventResponse* response) {
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
	
	void LogEventRequest_Response(GS& gsInstance, const LogEventResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	LogEventRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetEventKey(eventKey)
	request.Send(LogEventRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.LogEventRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.LogEventResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createLogEventRequest()
	.setAnalyticsData(analyticsData)
	.setEventKey(eventKey)
	.send(new GSEventListener<LogEventResponse>() {
		@Override
		public void onEvent(LogEventResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.LogEventRequest();
	request.analyticsData = ...;
	request.eventKey = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


