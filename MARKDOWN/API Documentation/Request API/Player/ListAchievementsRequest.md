
# ListAchievementsRequest


Retrieves a list of the configured achievements in the game, along with whether the current player has earned the achievement.


<a href="https://api.gamesparks.net/#listachievementsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A reponse containing the game's achievments and an indication of whether the player has earned it

Parameter | Type | Description
--------- | ---- | -----------
achievements | [Achievement[]](#achievement) | A list of JSON achievment objects
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### Achievement

A nested object that represents the achievement data.

Parameter | Type | Description
--------- | ---- | -----------
description | string | The desciption of the Achievement
earned | boolean | Whether to current player has earned the achievement
name | string | The name of the Achievement
propertySet | JSON | The custom property set configured on this Achievement
shortCode | string | The shortCode of the Achievement

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
	new ListAchievementsRequest()
		.Send((response) => {
		GSEnumerable<var> achievements = response.Achievements; 
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
	    .createListAchievementsRequest()
		.send(function(response:com.gamesparks.api.responses.ListAchievementsResponse):void {
		var achievements:Vector.<Achievement> = response.getAchievements(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListAchievementsRequest* request = [[GSListAchievementsRequest alloc] init];
	[request setCallback:^ (GSListAchievementsResponse* response) {
	NSArray* achievements = [response getAchievements]; 
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
	
	void ListAchievementsRequest_Response(GS& gsInstance, const ListAchievementsResponse& response) {
	gsstl:vector<Types::Achievement*> achievements = response.getAchievements(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListAchievementsRequest request(gsInstance);
	request.Send(ListAchievementsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListAchievementsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListAchievementsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListAchievementsRequest()
	.send(new GSEventListener<ListAchievementsResponse>() {
		@Override
		public void onEvent(ListAchievementsResponse response) {
			List<Achievement> achievements = response.getAchievements(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListAchievementsRequest();
	var response = request.Send();
	
var achievements = response.achievements; 
var scriptData = response.scriptData; 
```


