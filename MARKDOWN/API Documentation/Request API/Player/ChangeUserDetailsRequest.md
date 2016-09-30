---
src: /API Documentation/Request API/Player/ChangeUserDetailsRequest.md
---

# ChangeUserDetailsRequest


Change the display name of the currently signed in Player.


<a href="https://api.gamesparks.net/#changeuserdetailsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
displayName | No | string | The new display name to set in the player data.
language | No | string | The new language code to set in the player data.
newPassword | No | string | The new password to set in the player data.
oldPassword | No | string | The player's existing password. If supplied it will be checked against the password stored in the player data. This allows you re-authenticate the player making the change.
userName | No | string | The new userName with which this player will sign in.  If the player currently authenticates using device authentication this will upgrade their account and require them to use username and password authentication from now on.

## Response Parameters


A response to a change user details request

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
DETAILS | UNRECOGNISED | The oldPassword did not match the one stored against the player.
USERNAME | TAKEN | The userName supplied is already in use.

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ChangeUserDetailsRequest()
		.SetAnalyticsData(analyticsData)
		.SetDisplayName(displayName)
		.SetLanguage(language)
		.SetNewPassword(newPassword)
		.SetOldPassword(oldPassword)
		.SetUserName(userName)
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
	    .createChangeUserDetailsRequest()
		.setAnalyticsData(analyticsData)
		.setDisplayName(displayName)
		.setLanguage(language)
		.setNewPassword(newPassword)
		.setOldPassword(oldPassword)
		.setUserName(userName)
		.send(function(response:com.gamesparks.api.responses.ChangeUserDetailsResponse):void {
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSChangeUserDetailsRequest* request = [[GSChangeUserDetailsRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setDisplayName:displayName;
	[request setLanguage:language;
	[request setNewPassword:newPassword;
	[request setOldPassword:oldPassword;
	[request setUserName:userName;
	[request setCallback:^ (GSChangeUserDetailsResponse* response) {
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
	
	void ChangeUserDetailsRequest_Response(GS& gsInstance, const ChangeUserDetailsResponse& response) {
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ChangeUserDetailsRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetDisplayName(displayName)
	request.SetLanguage(language)
	request.SetNewPassword(newPassword)
	request.SetOldPassword(oldPassword)
	request.SetUserName(userName)
	request.Send(ChangeUserDetailsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ChangeUserDetailsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ChangeUserDetailsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createChangeUserDetailsRequest()
	.setAnalyticsData(analyticsData)
	.setDisplayName(displayName)
	.setLanguage(language)
	.setNewPassword(newPassword)
	.setOldPassword(oldPassword)
	.setUserName(userName)
	.send(new GSEventListener<ChangeUserDetailsResponse>() {
		@Override
		public void onEvent(ChangeUserDetailsResponse response) {
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ChangeUserDetailsRequest();
	request.analyticsData = ...;
	request.displayName = ...;
	request.language = ...;
	request.newPassword = ...;
	request.oldPassword = ...;
	request.userName = ...;
	var response = request.Send();
	
var scriptData = response.scriptData; 
```


