---
src: /API Documentation/Request API/Player/ListGameFriendsRequest.md
---

# ListGameFriendsRequest


Returns the list of the current players game friends.

A Game friend is someone in their social network who also plays the game.

Against each friend, an indicator is supplied to show whether the friend is currently connected to the GameSparks service


<a href="https://api.gamesparks.net/#listgamefriendsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A response containing the list of the current players game friends.

Parameter | Type | Description
--------- | ---- | -----------
friends | [Player[]](#player) | A list of JSON objects containing game friend data
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### Player

A nested object that represents a player.

Parameter | Type | Description
--------- | ---- | -----------
achievements | string[] | The achievements of the Player
displayName | string | The display name of the Player
externalIds | JSON | The external Id's of the Player
id | string | The id of the Player
online | boolean | The online status of the Player
scriptData | JSON | The script data of the Player
virtualGoods | string[] | The virtual goods of the Player

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
	new ListGameFriendsRequest()
		.Send((response) => {
		GSEnumerable<var> friends = response.Friends; 
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
	    .createListGameFriendsRequest()
		.send(function(response:com.gamesparks.api.responses.ListGameFriendsResponse):void {
		var friends:Vector.<Player> = response.getFriends(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListGameFriendsRequest* request = [[GSListGameFriendsRequest alloc] init];
	[request setCallback:^ (GSListGameFriendsResponse* response) {
	NSArray* friends = [response getFriends]; 
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
	
	void ListGameFriendsRequest_Response(GS& gsInstance, const ListGameFriendsResponse& response) {
	gsstl:vector<Types::Player*> friends = response.getFriends(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListGameFriendsRequest request(gsInstance);
	request.Send(ListGameFriendsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListGameFriendsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListGameFriendsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListGameFriendsRequest()
	.send(new GSEventListener<ListGameFriendsResponse>() {
		@Override
		public void onEvent(ListGameFriendsResponse response) {
			List<Player> friends = response.getFriends(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListGameFriendsRequest();
	var response = request.Send();
	
var friends = response.friends; 
var scriptData = response.scriptData; 
```


