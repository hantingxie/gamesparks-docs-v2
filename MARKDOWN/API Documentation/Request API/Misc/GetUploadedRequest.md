---
src: /API Documentation/Request API/Misc/GetUploadedRequest.md
---

# GetUploadedRequest


Returns a secure, time sensitive URL to a piece of content that was previously uploaded to the GameSparks platform by a player.


<a href="https://api.gamesparks.net/#getuploadedrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
uploadId | No | string | The system generated id of the uploaded item

## Response Parameters


A reponse containing a time sensitive URL to a piece of content that was previously uploaded to the GameSparks platform by a player.

Parameter | Type | Description
--------- | ---- | -----------
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
size | number | The size of the file in bytes
url | string | A time sensitive URL to a piece of content

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
uploadId | INVALID | The upload id was invalid

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GetUploadedRequest()
		.SetUploadId(uploadId)
		.Send((response) => {
		GSData scriptData = response.ScriptData; 
		var size = response.Size; 
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
	    .createGetUploadedRequest()
		.setUploadId(uploadId)
		.send(function(response:com.gamesparks.api.responses.GetUploadedResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		var size:Number = response.getSize(); 
		var url:String = response.getUrl(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetUploadedRequest* request = [[GSGetUploadedRequest alloc] init];
	[request setUploadId:uploadId;
	[request setCallback:^ (GSGetUploadedResponse* response) {
	NSDictionary* scriptData = [response getScriptData]; 
	NSNumber* size = [response getSize]; 
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
	
	void GetUploadedRequest_Response(GS& gsInstance, const GetUploadedResponse& response) {
	GSData scriptData = response.getScriptData(); 
	Optional::t_LongOptional size = response.getSize(); 
	gsstl::string url = response.getUrl(); 
	}
	......
	
	GetUploadedRequest request(gsInstance);
	request.SetUploadId(uploadId)
	request.Send(GetUploadedRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetUploadedRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetUploadedResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetUploadedRequest()
	.setUploadId(uploadId)
	.send(new GSEventListener<GetUploadedResponse>() {
		@Override
		public void onEvent(GetUploadedResponse response) {
			GSData scriptData = response.getScriptData(); 
			Long size = response.getSize(); 
			String url = response.getUrl(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetUploadedRequest();
	request.uploadId = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
var size = response.size; 
var url = response.url; 
```


