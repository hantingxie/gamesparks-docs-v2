
# GetPropertyRequest


Get the property for the given short Code.


<a href="https://api.gamesparks.net/#getpropertyrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
propertyShortCode | Yes | string | The shortCode of the property to return.

## Response Parameters


A response containing the requested property

Parameter | Type | Description
--------- | ---- | -----------
property | JSON | The property value
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
property | NOT_FOUND | No property with given shortCode could be found.

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GetPropertyRequest()
		.SetPropertyShortCode(propertyShortCode)
		.Send((response) => {
		GSData property = response.Property; 
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
	    .createGetPropertyRequest()
		.setPropertyShortCode(propertyShortCode)
		.send(function(response:com.gamesparks.api.responses.GetPropertyResponse):void {
		var property:Object = response.getProperty(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetPropertyRequest* request = [[GSGetPropertyRequest alloc] init];
	[request setPropertyShortCode:propertyShortCode;
	[request setCallback:^ (GSGetPropertyResponse* response) {
	NSDictionary* property = [response getProperty]; 
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
	
	void GetPropertyRequest_Response(GS& gsInstance, const GetPropertyResponse& response) {
	GSData property = response.getProperty(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	GetPropertyRequest request(gsInstance);
	request.SetPropertyShortCode(propertyShortCode)
	request.Send(GetPropertyRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetPropertyRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetPropertyResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetPropertyRequest()
	.setPropertyShortCode(propertyShortCode)
	.send(new GSEventListener<GetPropertyResponse>() {
		@Override
		public void onEvent(GetPropertyResponse response) {
			GSData property = response.getProperty(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetPropertyRequest();
	request.propertyShortCode = ...;
	var response = request.Send();
	
var property = response.property; 
var scriptData = response.scriptData; 
```


