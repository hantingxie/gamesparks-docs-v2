---
src: /API Documentation/Request API/Admin/ScheduleBulkJobAdminRequest.md
---

# ScheduleBulkJobAdminRequest


Schedules a bulk job to be run against multiple players.


<a href="https://api.gamesparks.net/#schedulebulkjobadminrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
data | No | DBObject | Optional data to be passed into the script
moduleShortCode | No | string | The short code of the cloud code module to be executed against each player
playerQuery | Yes | DBObject | The query to be run against the player collection to identify which players to execute the cloud code for
scheduledTime | No | date | An optional date and time for this job to be run
script | No | string | The script to be executed against each player

## Response Parameters


A response acknowledging the scheduling of a bulk job

Parameter | Type | Description
--------- | ---- | -----------
estimatedCount | number | The count of players who would be affected by this job if it ran at the time it was submitted
jobId | string | The unique job ID, used to identify this job in future requests
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
moduleShortCode | INVALID | One of either the script or moduleShortCode properties must be populated
script | Validation error | If an invalid script is supplied, the validation error will be returned here.
scheduledTime | INVALID | The date/time for scheduled jobs must not be in the past

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ScheduleBulkJobAdminRequest()
		.SetAnalyticsData(analyticsData)
		.SetData(data)
		.SetModuleShortCode(moduleShortCode)
		.SetPlayerQuery(playerQuery)
		.SetScheduledTime(scheduledTime)
		.SetScript(script)
		.Send((response) => {
		long? estimatedCount = response.EstimatedCount; 
		string jobId = response.JobId; 
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
	    .createScheduleBulkJobAdminRequest()
		.setAnalyticsData(analyticsData)
		.setData(data)
		.setModuleShortCode(moduleShortCode)
		.setPlayerQuery(playerQuery)
		.setScheduledTime(scheduledTime)
		.setScript(script)
		.send(function(response:com.gamesparks.api.responses.ScheduleBulkJobAdminResponse):void {
		var estimatedCount:Number = response.getEstimatedCount(); 
		var jobId:String = response.getJobId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSScheduleBulkJobAdminRequest* request = [[GSScheduleBulkJobAdminRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setData:data;
	[request setModuleShortCode:moduleShortCode;
	[request setPlayerQuery:playerQuery;
	[request setScheduledTime:scheduledTime;
	[request setScript:script;
	[request setCallback:^ (GSScheduleBulkJobAdminResponse* response) {
	NSNumber* estimatedCount = [response getEstimatedCount]; 
	NSString* jobId = [response getJobId]; 
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
	
	void ScheduleBulkJobAdminRequest_Response(GS& gsInstance, const ScheduleBulkJobAdminResponse& response) {
	Optional::t_LongOptional estimatedCount = response.getEstimatedCount(); 
	gsstl::string jobId = response.getJobId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ScheduleBulkJobAdminRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetData(data)
	request.SetModuleShortCode(moduleShortCode)
	request.SetPlayerQuery(playerQuery)
	request.SetScheduledTime(scheduledTime)
	request.SetScript(script)
	request.Send(ScheduleBulkJobAdminRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ScheduleBulkJobAdminRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ScheduleBulkJobAdminResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createScheduleBulkJobAdminRequest()
	.setAnalyticsData(analyticsData)
	.setData(data)
	.setModuleShortCode(moduleShortCode)
	.setPlayerQuery(playerQuery)
	.setScheduledTime(scheduledTime)
	.setScript(script)
	.send(new GSEventListener<ScheduleBulkJobAdminResponse>() {
		@Override
		public void onEvent(ScheduleBulkJobAdminResponse response) {
			Long estimatedCount = response.getEstimatedCount(); 
			String jobId = response.getJobId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ScheduleBulkJobAdminRequest();
	request.analyticsData = ...;
	request.data = ...;
	request.moduleShortCode = ...;
	request.playerQuery = ...;
	request.scheduledTime = ...;
	request.script = ...;
	var response = request.Send();
	
var estimatedCount = response.estimatedCount; 
var jobId = response.jobId; 
var scriptData = response.scriptData; 
```


