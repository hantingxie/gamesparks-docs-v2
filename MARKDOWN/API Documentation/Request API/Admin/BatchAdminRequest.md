
# BatchAdminRequest


Performs a request for multiple players.


<a href="https://api.gamesparks.net/#batchadminrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
playerIds | Yes | string[] | The players to run the request for.
request | Yes | DBObject | The request to be run for each player.

## Response Parameters


A response containing the individual responses for requests performed via a BatchAdminRequest

Parameter | Type | Description
--------- | ---- | -----------
responses | JSON | A map of responses by player ID
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
playerIds | INVALID | Between 1-500 player IDs must be supplied in the form of an array
request | INVALID | You must supply a valid request in JSON format to be performed for each player listed in playerIds

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new BatchAdminRequest()
		.SetAnalyticsData(analyticsData)
		.SetPlayerIds(playerIds)
		.SetRequest(request)
		.Send((response) => {
		GSData responses = response.Responses; 
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
	    .createBatchAdminRequest()
		.setAnalyticsData(analyticsData)
		.setPlayerIds(playerIds)
		.setRequest(request)
		.send(function(response:com.gamesparks.api.responses.BatchAdminResponse):void {
		var responses:Object = response.getResponses(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSBatchAdminRequest* request = [[GSBatchAdminRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setPlayerIds:playerIds;
	[request setRequest:request;
	[request setCallback:^ (GSBatchAdminResponse* response) {
	NSDictionary* responses = [response getResponses]; 
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
	
	void BatchAdminRequest_Response(GS& gsInstance, const BatchAdminResponse& response) {
	GSData responses = response.getResponses(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	BatchAdminRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetPlayerIds(playerIds)
	request.SetRequest(request)
	request.Send(BatchAdminRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.BatchAdminRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.BatchAdminResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createBatchAdminRequest()
	.setAnalyticsData(analyticsData)
	.setPlayerIds(playerIds)
	.setRequest(request)
	.send(new GSEventListener<BatchAdminResponse>() {
		@Override
		public void onEvent(BatchAdminResponse response) {
			GSData responses = response.getResponses(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.BatchAdminRequest();
	request.analyticsData = ...;
	request.playerIds = ...;
	request.request = ...;
	var response = request.Send();
	
var responses = response.responses; 
var scriptData = response.scriptData; 
```


