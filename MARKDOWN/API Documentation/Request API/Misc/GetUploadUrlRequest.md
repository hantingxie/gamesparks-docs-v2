---
src: /API Documentation/Request API/Misc/GetUploadUrlRequest.md
---

# GetUploadUrlRequest


Returns a secure, time sensitive URL to allow the game to upload a piece of player content to the GameSparks platform.


<a href="https://api.gamesparks.net/#getuploadurlrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
uploadData | No | JSON[] | Optional meta data which is stored against the player's uploaded content

## Response Parameters


A response containing a time sensitive URL to allow the game to upload a piece of player content to the GameSparks platform

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
url | string | The time sensitive upload URL

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
	new GetUploadUrlRequest()
		.SetAnalyticsData(analyticsData)
		.SetUploadData(uploadData)
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
		string url = response.Url; 
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
	    .createGetUploadUrlRequest()
		.setAnalyticsData(analyticsData)
		.setUploadData(uploadData)
		.send(function(response:com.gamesparks.api.responses.GetUploadUrlResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var url:String = response.getUrl(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetUploadUrlRequest* request = [[GSGetUploadUrlRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setUploadData:uploadData;
	[request setCallback:^ (GSGetUploadUrlResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
	NSString* url = [response getUrl]; 
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
	
	void GetUploadUrlRequest_Response(GS& gsInstance, const GetUploadUrlResponse& response) {
	GSData scriptData = response.getScriptData(); 
	gsstl::string url = response.getUrl(); 
	}
	......
	
	GetUploadUrlRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetUploadData(uploadData)
	request.Send(GetUploadUrlRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetUploadUrlRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetUploadUrlResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetUploadUrlRequest()
	.setAnalyticsData(analyticsData)
	.setUploadData(uploadData)
	.send(new GSEventListener<GetUploadUrlResponse>() {
		@Override
		public void onEvent(GetUploadUrlResponse response) {
			GSData scriptData = response.getScriptData(); 
			String url = response.getUrl(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetUploadUrlRequest();
	request.analyticsData = ...;
	request.uploadData = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
var url = response.url; 
```


