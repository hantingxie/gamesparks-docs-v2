
# FindChallengeRequest


Allows a player to find challenges that they are eligible to join.


<a href="https://api.gamesparks.net/#findchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
accessType | Yes | string | The type of challenge to find, either PUBLIC or FRIENDS.  Defaults to FRIENDS
count | No | number | The number of challenges to return (MAX=50)
eligibility | Yes | JSON | Optional.  Allows the current player's eligibility to be overridden by what is provided here.
offset | No | number | The offset to start from when returning challenges (used for paging)
shortCode | No | string[] | Optional shortCodes to filter the results by challenge type

## Response Parameters


A response to a find challenge request

Parameter | Type | Description
--------- | ---- | -----------
challengeInstances | [Challenge[]](#challenge) | A list of JSON objects representing the challenges.
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

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

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### PlayerTurnCount

Represents the number of turns a player has taken in a turn based challenge.

Parameter | Type | Description
--------- | ---- | -----------
count | string | The number of turns that the player has taken so far during this challenge.
playerId | string | The unique player id.

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
eligibility | { "XXX" : "UNRECOGNISED"} | XXX is not a valid field of eligibility
eligibility | { "segments" : {"XXX" : "MALFORMED"}} | The value provied for XXX is not in the correct format

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new FindChallengeRequest()
		.SetAccessType(accessType)
		.SetCount(count)
		.SetEligibility(eligibility)
		.SetOffset(offset)
		.SetShortCode(shortCode)
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
	    .createFindChallengeRequest()
		.setAccessType(accessType)
		.setCount(count)
		.setEligibility(eligibility)
		.setOffset(offset)
		.setShortCode(shortCode)
		.send(function(response:com.gamesparks.api.responses.FindChallengeResponse):void {
		var challengeInstances:Vector.<Challenge> = response.getChallengeInstances(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSFindChallengeRequest* request = [[GSFindChallengeRequest alloc] init];
	[request setAccessType:accessType;
	[request setCount:count;
	[request setEligibility:eligibility;
	[request setOffset:offset;
	[request setShortCode:shortCode;
	[request setCallback:^ (GSFindChallengeResponse* response) {
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
	
	void FindChallengeRequest_Response(GS& gsInstance, const FindChallengeResponse& response) {
	gsstl:vector<Types::Challenge*> challengeInstances = response.getChallengeInstances(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	FindChallengeRequest request(gsInstance);
	request.SetAccessType(accessType)
	request.SetCount(count)
	request.SetEligibility(eligibility)
	request.SetOffset(offset)
	request.SetShortCode(shortCode)
	request.Send(FindChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.FindChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.FindChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createFindChallengeRequest()
	.setAccessType(accessType)
	.setCount(count)
	.setEligibility(eligibility)
	.setOffset(offset)
	.setShortCode(shortCode)
	.send(new GSEventListener<FindChallengeResponse>() {
		@Override
		public void onEvent(FindChallengeResponse response) {
			List<Challenge> challengeInstances = response.getChallengeInstances(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.FindChallengeRequest();
	request.accessType = ...;
	request.count = ...;
	request.eligibility = ...;
	request.offset = ...;
	request.shortCode = ...;
	var response = request.Send();
	
var challengeInstances = response.challengeInstances; 
var scriptData = response.scriptData; 
```


