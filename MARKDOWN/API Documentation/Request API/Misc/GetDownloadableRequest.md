---
src: /API Documentation/Request API/Misc/GetDownloadableRequest.md
---

# GetDownloadableRequest


Returns a secure, time sensitive url to allow the game to download a piece of downloadable content stored in the GameSparks platform.


<a href="https://api.gamesparks.net/#getdownloadablerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
shortCode | Yes | string | The short code of the Downloadable item

## Response Parameters


A response containing the download URL for a downloadable item

Parameter | Type | Description
--------- | ---- | -----------
lastModified | date | The date when the downloadable item was last modified
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
shortCode | string | The short code of the item
size | number | The size of the item in bytes
url | string | The download URL

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
shortCode | INVALID | The short code does not match any Downloadable shortCode

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GetDownloadableRequest()
		.SetAnalyticsData(analyticsData)
		.SetShortCode(shortCode)
		.Send((response) => {
		DateTime? lastModified = response.LastModified; 
		GSData scriptData = response.ScriptData; 
		string shortCode = response.ShortCode; 
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
	    .createGetDownloadableRequest()
		.setAnalyticsData(analyticsData)
		.setShortCode(shortCode)
		.send(function(response:com.gamesparks.api.responses.GetDownloadableResponse):void {
		var lastModified:Date = response.getLastModified(); 
		var scriptData:ScriptData = response.getScriptData(); 
		var shortCode:String = response.getShortCode(); 
		var size:Number = response.getSize(); 
		var url:String = response.getUrl(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetDownloadableRequest* request = [[GSGetDownloadableRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setShortCode:shortCode;
	[request setCallback:^ (GSGetDownloadableResponse* response) {
	NSDate* lastModified = [response getLastModified]; 
	NSDictionary* scriptData = [response getScriptData]; 
	NSString* shortCode = [response getShortCode]; 
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
	
	void GetDownloadableRequest_Response(GS& gsInstance, const GetDownloadableResponse& response) {
	GSDateTime::t_Optional lastModified = response.getLastModified(); 
	GSData scriptData = response.getScriptData(); 
	gsstl::string shortCode = response.getShortCode(); 
	Optional::t_LongOptional size = response.getSize(); 
	gsstl::string url = response.getUrl(); 
	}
	......
	
	GetDownloadableRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetShortCode(shortCode)
	request.Send(GetDownloadableRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetDownloadableRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetDownloadableResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetDownloadableRequest()
	.setAnalyticsData(analyticsData)
	.setShortCode(shortCode)
	.send(new GSEventListener<GetDownloadableResponse>() {
		@Override
		public void onEvent(GetDownloadableResponse response) {
			Date lastModified = response.getLastModified(); 
			GSData scriptData = response.getScriptData(); 
			String shortCode = response.getShortCode(); 
			Long size = response.getSize(); 
			String url = response.getUrl(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetDownloadableRequest();
	request.analyticsData = ...;
	request.shortCode = ...;
	var response = request.Send();
	
var lastModified = response.lastModified; 
var scriptData = response.scriptData; 
var shortCode = response.shortCode; 
var size = response.size; 
var url = response.url; 
```


