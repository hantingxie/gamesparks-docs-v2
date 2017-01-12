
# ListChallengeTypeRequest


Returns the list of configured challenge types.


<a href="https://api.gamesparks.net/#listchallengetyperequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A response containing the list of configured challenge types in the game

Parameter | Type | Description
--------- | ---- | -----------
challengeTemplates | [ChallengeType[]](#challengetype) | A list of JSON objects containing the challenge templates for the game
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ChallengeType



Parameter | Type | Description
--------- | ---- | -----------
challengeShortCode | string | The shortCode for this challenge.
description | string | The description of this challenge.
getleaderboardName | string | The name of the leaderboard for this challenge.
name | string | The name of this challenge.
tags | string | The tags for this challenge.

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
	new ListChallengeTypeRequest()
		.Send((response) => {
		GSEnumerable<var> challengeTemplates = response.ChallengeTemplates; 
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
	    .createListChallengeTypeRequest()
		.send(function(response:com.gamesparks.api.responses.ListChallengeTypeResponse):void {
		var challengeTemplates:Vector.<ChallengeType> = response.getChallengeTemplates(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListChallengeTypeRequest* request = [[GSListChallengeTypeRequest alloc] init];
	[request setCallback:^ (GSListChallengeTypeResponse* response) {
	NSArray* challengeTemplates = [response getChallengeTemplates]; 
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
	
	void ListChallengeTypeRequest_Response(GS& gsInstance, const ListChallengeTypeResponse& response) {
	gsstl:vector<Types::ChallengeType*> challengeTemplates = response.getChallengeTemplates(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListChallengeTypeRequest request(gsInstance);
	request.Send(ListChallengeTypeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListChallengeTypeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListChallengeTypeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListChallengeTypeRequest()
	.send(new GSEventListener<ListChallengeTypeResponse>() {
		@Override
		public void onEvent(ListChallengeTypeResponse response) {
			List<ChallengeType> challengeTemplates = response.getChallengeTemplates(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListChallengeTypeRequest();
	var response = request.Send();
	
var challengeTemplates = response.challengeTemplates; 
var scriptData = response.scriptData; 
```


