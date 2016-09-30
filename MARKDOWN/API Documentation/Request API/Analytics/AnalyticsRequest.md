---
src: /API Documentation/Request API/Analytics/AnalyticsRequest.md
---

# AnalyticsRequest


Records some custom analytical data.

Simple analytics, where you just need to track the number of times something happened, just take a key parameter. We'll record the players id against the data to allow you to report on averages per user

Timed analytics allow you to send start and end timer requests, and with this data GameSparks can track the length of time something takes.

If an end request is sent without a matching start timer the request will fail silently and your analytics data might not contain what you expect.

If both start and end are supplied, the request will be treated as a start timer.

An additional data payload can be attached to the event for advanced reporting. This data can be a string, number or JSON object.

If a second start timer is created using a key that has already had a start timer created without an end, the previous one will be marked as abandoned.


<a href="https://api.gamesparks.net/#analyticsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
data | No | JSON | Custom data payload
end | No | boolean | Use the value true to indicate it's an end timer
key | No | string | The key you want to track this analysis with.
start | No | boolean | Use the value true to indicate it's a start timer

## Response Parameters


A response to an analytics request

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
	new AnalyticsRequest()
		.SetAnalyticsData(analyticsData)
		.SetData(data)
		.SetEnd(end)
		.SetKey(key)
		.SetStart(start)
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
	    .createAnalyticsRequest()
		.setAnalyticsData(analyticsData)
		.setData(data)
		.setEnd(end)
		.setKey(key)
		.setStart(start)
		.send(function(response:com.gamesparks.api.responses.AnalyticsResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSAnalyticsRequest* request = [[GSAnalyticsRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setData:data;
	[request setEnd:end;
	[request setKey:key;
	[request setStart:start;
	[request setCallback:^ (GSAnalyticsResponse* response) {
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
	
	void AnalyticsRequest_Response(GS& gsInstance, const AnalyticsResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	AnalyticsRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetData(data)
	request.SetEnd(end)
	request.SetKey(key)
	request.SetStart(start)
	request.Send(AnalyticsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.AnalyticsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AnalyticsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createAnalyticsRequest()
	.setAnalyticsData(analyticsData)
	.setData(data)
	.setEnd(end)
	.setKey(key)
	.setStart(start)
	.send(new GSEventListener<AnalyticsResponse>() {
		@Override
		public void onEvent(AnalyticsResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.AnalyticsRequest();
	request.analyticsData = ...;
	request.data = ...;
	request.end = ...;
	request.key = ...;
	request.start = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


