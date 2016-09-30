---
src: /API Documentation/Request API/Player/ListInviteFriendsRequest.md
---

# ListInviteFriendsRequest


Returns the list of the current players friends in their social network, who are not yet playing this game.

This is dependent on the security and privacy policies of the social network.

For example, Facebook's policies prevent this friend list being provided, whereas Twitter will supply a list of users who are not playing the game.


<a href="https://api.gamesparks.net/#listinvitefriendsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics

## Response Parameters


A response containing a list of non game friends.

Parameter | Type | Description
--------- | ---- | -----------
friends | [InvitableFriend[]](#invitablefriend) | A list of JSON objects containing game friend data
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### InvitableFriend

A nested object that represents the invitable friend.

Parameter | Type | Description
--------- | ---- | -----------
displayName | string | The display name of the External Friend
id | string | The ID of the External Friend
profilePic | string | The profile picture URL of the External Friend


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ListInviteFriendsRequest()
		.SetAnalyticsData(analyticsData)
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
	    .createListInviteFriendsRequest()
		.setAnalyticsData(analyticsData)
		.send(function(response:com.gamesparks.api.responses.ListInviteFriendsResponse):void {
		var friends:Vector.<InvitableFriend> = response.getFriends(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListInviteFriendsRequest* request = [[GSListInviteFriendsRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setCallback:^ (GSListInviteFriendsResponse* response) {
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
	
	void ListInviteFriendsRequest_Response(GS& gsInstance, const ListInviteFriendsResponse& response) {
	gsstl:vector<Types::InvitableFriend*> friends = response.getFriends(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListInviteFriendsRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.Send(ListInviteFriendsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListInviteFriendsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListInviteFriendsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListInviteFriendsRequest()
	.setAnalyticsData(analyticsData)
	.send(new GSEventListener<ListInviteFriendsResponse>() {
		@Override
		public void onEvent(ListInviteFriendsResponse response) {
			List<InvitableFriend> friends = response.getFriends(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListInviteFriendsRequest();
	request.analyticsData = ...;
	var response = request.Send();
	
var friends = response.friends; 
var scriptData = response.scriptData; 
```


