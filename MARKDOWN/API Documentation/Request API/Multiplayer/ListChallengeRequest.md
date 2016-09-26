---
src: /API Documentation/Request API/Multiplayer/ListChallengeRequest.md
---

# ListChallengeRequest


Returns a list of challenges in the state defined in the 'state' field.

The response can be further filtered by passing a shortCode field which will limit the returned lists to challenges of that short code.

Valid states are:

WAITING : The challenge has been issued and accepted and is waiting for the start date.

RUNNING : The challenge is active.

ISSUED : The challenge has been issued by the current player and is waiting to be accepted.

RECEIVED : The challenge has been issued to the current player and is waiting to be accepted.

COMPLETE : The challenge has completed.

DECLINED : The challenge has been issued by the current player and has been declined.


<a href="https://api.gamesparks.net/#listchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
entryCount | No | number | The number of items to return in a page (default=50)
offset | No | number | The offset (page number) to start from (default=0)
shortCode | No | string | The type of challenge to return
state | No | string | The state of the challenged to be returned
states | No | string[] | The states of the challenges to be returned

## Response Parameters


A response containing challenges that are in the state that was specified in the request

Parameter | Type | Description
--------- | ---- | -----------
challengeInstances | [Challenge[]](#challenge) | A list of JSON objects representing the challenges.
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### PlayerTurnCount

Represents the number of turns a player has taken in a turn based challenge.

Parameter | Type | Description
--------- | ---- | -----------
count | string | The number of turns that the player has taken so far during this challenge.
playerId | string | The unique player id.

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### PlayerDetail

An object representing a player's id and name

Parameter | Type | Description
--------- | ---- | -----------
externalIds | JSON | A player's external identifiers
id | string | A player's id
name | string | A player's name

### Challenge

A nested object that represents the challenge data.

Parameter | Type | Description
--------- | ---- | -----------
accepted | [PlayerDetail[]](#playerdetail) | A list of PlayerDetail objects that represents the players that have accepted this challenge.
challengeId | string | A unique identifier for this challenge.
challengeMessage | string | The message included in the challenge by the challenging player who created the challenge.
challengeName | string | The name of the challenge that this message relates to.
challenged | [PlayerDetail[]](#playerdetail) | A list of PlayerDetail objects that represents the players that were challenged in this challenge.
challenger | [PlayerDetail](#playerdetail) | Details of the player who issued this challenge.
currency1Wager | number | The amount of type 1 currency that has been wagered on this challenge.
currency2Wager | number | The amount of type 2 currency that has been wagered on this challenge.
currency3Wager | number | The amount of type 3 currency that has been wagered on this challenge.
currency4Wager | number | The amount of type 4 currency that has been wagered on this challenge.
currency5Wager | number | The amount of type 5 currency that has been wagered on this challenge.
currency6Wager | number | The amount of type 6 currency that has been wagered on this challenge.
declined | [PlayerDetail[]](#playerdetail) | A list of PlayerDetail objects that represents the players that have declined this challenge.
endDate | date | The date when the challenge ends.
expiryDate | date | The latest date that a player can accept the challenge.
maxTurns | number | The maximum number of turns that this challenge is configured for.
nextPlayer | string | In a turn based challenge this fields contains the player's id whose turn it is next.
scriptData | ScriptData[] | ScriptData is arbitrary data that can be stored in a challenge instance by a Cloud Code script.
shortCode | string | The challenge's short code.
startDate | date | The date when the challenge starts.
state | string | One of these possible state values: ISSUED, EXPIRED, ACCEPTED, DECLINED, COMPLETE, WITHDRAWN, RUNNING, WAITING, RECEIVED
turnCount | [PlayerTurnCount[]](#playerturncount) | A collection containing the number of turns taken by each player that has accepted the challenge.


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new ListChallengeRequest()
		.SetEntryCount(entryCount)
		.SetOffset(offset)
		.SetShortCode(shortCode)
		.SetState(state)
		.SetStates(states)
		.Send((response) => {
		GSEnumerable<var> challengeInstances = response.ChallengeInstances; 
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
	    .createListChallengeRequest()
		.setEntryCount(entryCount)
		.setOffset(offset)
		.setShortCode(shortCode)
		.setState(state)
		.setStates(states)
		.send(function(response:com.gamesparks.api.responses.ListChallengeResponse):void {
		var challengeInstances:Vector.<Challenge> = response.getChallengeInstances(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSListChallengeRequest* request = [[GSListChallengeRequest alloc] init];
	[request setEntryCount:entryCount;
	[request setOffset:offset;
	[request setShortCode:shortCode;
	[request setState:state;
	[request setStates:states;
	[request setCallback:^ (GSListChallengeResponse* response) {
	NSArray* challengeInstances = [response getChallengeInstances]; 
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
	
	void ListChallengeRequest_Response(GS& gsInstance, const ListChallengeResponse& response) {
	gsstl:vector<Types::Challenge*> challengeInstances = response.getChallengeInstances(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	ListChallengeRequest request(gsInstance);
	request.SetEntryCount(entryCount)
	request.SetOffset(offset)
	request.SetShortCode(shortCode)
	request.SetState(state)
	request.SetStates(states)
	request.Send(ListChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.ListChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.ListChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createListChallengeRequest()
	.setEntryCount(entryCount)
	.setOffset(offset)
	.setShortCode(shortCode)
	.setState(state)
	.setStates(states)
	.send(new GSEventListener<ListChallengeResponse>() {
		@Override
		public void onEvent(ListChallengeResponse response) {
			List<Challenge> challengeInstances = response.getChallengeInstances(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.ListChallengeRequest();
	request.entryCount = ...;
	request.offset = ...;
	request.shortCode = ...;
	request.state = ...;
	request.states = ...;
	var response = request.Send();
	
var challengeInstances = response.challengeInstances; 
var scriptData = response.scriptData; 
```


