---
src: /API Documentation/Request API/Misc/PushRegistrationRequest.md
---

# PushRegistrationRequest


Registers the current device for push notifications. Currently GameSparks supports iOS, GCM & Microsoft Push notifications.

Supply the device type, and the push notification identifier for the device.


<a href="https://api.gamesparks.net/#pushregistrationrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
deviceOS | Yes | string | The type of id, valid values are ios, android, wp8, w8, kindle or viber
pushId | Yes | string | The push notification identifier for the device

## Response Parameters


A response to a push registration request 

Parameter | Type | Description
--------- | ---- | -----------
registrationId | string | An identifier for the successful registration.  Clients should store this value to be used in the event the player no longer wants to receive push notifications to this device.
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
deviceOS | IOS|ANDROID|WP8|W8|KINDLE|VIBER | deviceOS is not a valid value

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new PushRegistrationRequest()
		.SetDeviceOS(deviceOS)
		.SetPushId(pushId)
		.Send((response) => {
		string registrationId = response.RegistrationId; 
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
	    .createPushRegistrationRequest()
		.setDeviceOS(deviceOS)
		.setPushId(pushId)
		.send(function(response:com.gamesparks.api.responses.PushRegistrationResponse):void {
		var registrationId:String = response.getRegistrationId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSPushRegistrationRequest* request = [[GSPushRegistrationRequest alloc] init];
	[request setDeviceOS:deviceOS;
	[request setPushId:pushId;
	[request setCallback:^ (GSPushRegistrationResponse* response) {
	NSString* registrationId = [response getRegistrationId]; 
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
	
	void PushRegistrationRequest_Response(GS& gsInstance, const PushRegistrationResponse& response) {
	gsstl::string registrationId = response.getRegistrationId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	PushRegistrationRequest request(gsInstance);
	request.SetDeviceOS(deviceOS)
	request.SetPushId(pushId)
	request.Send(PushRegistrationRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.PushRegistrationRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.PushRegistrationResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createPushRegistrationRequest()
	.setDeviceOS(deviceOS)
	.setPushId(pushId)
	.send(new GSEventListener<PushRegistrationResponse>() {
		@Override
		public void onEvent(PushRegistrationResponse response) {
			String registrationId = response.getRegistrationId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.PushRegistrationRequest();
	request.deviceOS = ...;
	request.pushId = ...;
	var response = request.Send();
	
var registrationId = response.registrationId; 
var scriptData = response.scriptData; 
```


