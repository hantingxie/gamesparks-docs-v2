
# GetPropertySetRequest


Get the property set for the given short Code.


<a href="https://api.gamesparks.net/#getpropertysetrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
propertySetShortCode | Yes | string | The shortCode of the property set to return.

## Response Parameters


A response containing the requested property set

Parameter | Type | Description
--------- | ---- | -----------
propertySet | JSON | The property set
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
propertySet | NOT_FOUND | No propertySet with given shortCode could be found.

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GetPropertySetRequest()
		.SetPropertySetShortCode(propertySetShortCode)
		.Send((response) => {
		GSData propertySet = response.PropertySet; 
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
	    .createGetPropertySetRequest()
		.setPropertySetShortCode(propertySetShortCode)
		.send(function(response:com.gamesparks.api.responses.GetPropertySetResponse):void {
		var propertySet:Object = response.getPropertySet(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetPropertySetRequest* request = [[GSGetPropertySetRequest alloc] init];
	[request setPropertySetShortCode:propertySetShortCode;
	[request setCallback:^ (GSGetPropertySetResponse* response) {
	NSDictionary* propertySet = [response getPropertySet]; 
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
	
	void GetPropertySetRequest_Response(GS& gsInstance, const GetPropertySetResponse& response) {
	GSData propertySet = response.getPropertySet(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	GetPropertySetRequest request(gsInstance);
	request.SetPropertySetShortCode(propertySetShortCode)
	request.Send(GetPropertySetRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetPropertySetRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetPropertySetResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetPropertySetRequest()
	.setPropertySetShortCode(propertySetShortCode)
	.send(new GSEventListener<GetPropertySetResponse>() {
		@Override
		public void onEvent(GetPropertySetResponse response) {
			GSData propertySet = response.getPropertySet(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetPropertySetRequest();
	request.propertySetShortCode = ...;
	var response = request.Send();
	
var propertySet = response.propertySet; 
var scriptData = response.scriptData; 
```


