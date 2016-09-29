
# CancelBulkJobAdminRequest


Cancel one or more bulk jobs.


<a href="https://api.gamesparks.net/#cancelbulkjobadminrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
bulkJobIds | Yes | string[] | The IDs of existing bulk jobs to cancel

## Response Parameters


A response listing cancelled bulk jobs

Parameter | Type | Description
--------- | ---- | -----------
bulkJobs | [BulkJob[]](#bulkjob) | A list of JSON objects containing bulk jobs
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### BulkJob

A nested object that represents the bulk job.

Parameter | Type | Description
--------- | ---- | -----------
actualCount | number | The actual count of players affected by the bulk job (calculated when the job started to run)
completed | date | The time at which the bulk job completed execution
created | date | The time at which the bulk job was created
data | DBObject | Data to be passed into the Module or Script
doneCount | number | The number of players processed by the bulk job so far
errorCount | number | The number of errors encountered whilst running the Module or Script for players
estimatedCount | number | The estimated count of players affected by the bulk job (estimated when the job was submitted)
id | string | The ID for the bulk job
moduleShortCode | string | The Cloud Code Module to run for each player
playerQuery | DBObject | The query to identify players to perform the bulk job on
scheduledTime | date | The time at which the job was scheduled to run
script | string | The Cloud Code script to run for each player
started | date | The time at which the bulk job started to execute
state | string | The current state of the bulk job

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
bulkJobIds | REQUIRED | The bulkJobIds must be an array of one or more valid bulk job IDs

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new CancelBulkJobAdminRequest()
		.SetAnalyticsData(analyticsData)
		.SetBulkJobIds(bulkJobIds)
		.Send((response) => {
		GSEnumerable<var> bulkJobs = response.BulkJobs; 
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
	    .createCancelBulkJobAdminRequest()
		.setAnalyticsData(analyticsData)
		.setBulkJobIds(bulkJobIds)
		.send(function(response:com.gamesparks.api.responses.CancelBulkJobAdminResponse):void {
		var bulkJobs:Vector.<BulkJob> = response.getBulkJobs(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSCancelBulkJobAdminRequest* request = [[GSCancelBulkJobAdminRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setBulkJobIds:bulkJobIds;
	[request setCallback:^ (GSCancelBulkJobAdminResponse* response) {
	NSArray* bulkJobs = [response getBulkJobs]; 
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
	
	void CancelBulkJobAdminRequest_Response(GS& gsInstance, const CancelBulkJobAdminResponse& response) {
	gsstl:vector<Types::BulkJob*> bulkJobs = response.getBulkJobs(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	CancelBulkJobAdminRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetBulkJobIds(bulkJobIds)
	request.Send(CancelBulkJobAdminRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.CancelBulkJobAdminRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.CancelBulkJobAdminResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createCancelBulkJobAdminRequest()
	.setAnalyticsData(analyticsData)
	.setBulkJobIds(bulkJobIds)
	.send(new GSEventListener<CancelBulkJobAdminResponse>() {
		@Override
		public void onEvent(CancelBulkJobAdminResponse response) {
			List<BulkJob> bulkJobs = response.getBulkJobs(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.CancelBulkJobAdminRequest();
	request.analyticsData = ...;
	request.bulkJobIds = ...;
	var response = request.Send();
	
var bulkJobs = response.bulkJobs; 
var scriptData = response.scriptData; 
```


