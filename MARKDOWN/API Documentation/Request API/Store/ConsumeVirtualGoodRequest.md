---
src: /API Documentation/Request API/Store/ConsumeVirtualGoodRequest.md
---

# ConsumeVirtualGoodRequest


Consumes a given amount of the specified virtual good.


<a href="https://api.gamesparks.net/#consumevirtualgoodrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
quantity | Yes | number | The amount of virtual goods to be consumed
shortCode | Yes | string | The short code of the virtual good to be consumed

## Response Parameters


A response to a consume virtual goods response

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

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
qty | INSUFFICIENT | The player does not have sufficient virtual goods for shortcode specified

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ConsumeVirtualGoodRequest()
		.SetQuantity(quantity)
		.SetShortCode(shortCode)
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
	    .createConsumeVirtualGoodRequest()
		.setQuantity(quantity)
		.setShortCode(shortCode)
		.send(function(response:com.gamesparks.api.responses.ConsumeVirtualGoodResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSConsumeVirtualGoodRequest* request = [[GSConsumeVirtualGoodRequest alloc] init];
	[request setQuantity:quantity;
	[request setShortCode:shortCode;
	[request setCallback:^ (GSConsumeVirtualGoodResponse* response) {
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
	
	void ConsumeVirtualGoodRequest_Response(GS& gsInstance, const ConsumeVirtualGoodResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ConsumeVirtualGoodRequest request(gsInstance);
	request.SetQuantity(quantity)
	request.SetShortCode(shortCode)
	request.Send(ConsumeVirtualGoodRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ConsumeVirtualGoodRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ConsumeVirtualGoodResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createConsumeVirtualGoodRequest()
	.setQuantity(quantity)
	.setShortCode(shortCode)
	.send(new GSEventListener<ConsumeVirtualGoodResponse>() {
		@Override
		public void onEvent(ConsumeVirtualGoodResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ConsumeVirtualGoodRequest();
	request.quantity = ...;
	request.shortCode = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


