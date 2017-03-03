---
src: /API Documentation/Request API/Admin/RevokePurchaseGoodsRequest.md
---

# RevokePurchaseGoodsRequest


Revokes the purchase of a good. The items aquired will be removed from remaining items of the player.


<a href="https://api.gamesparks.net/#revokepurchasegoodsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
playerId | Yes | string | The playerId for which to revoke the transaction
storeType | Yes | string | The store type for which to revoke these transactions
transactionIds | Yes | string[] | The list of transactionIds to revoke

## Response Parameters


A response containing details of the revoked items

Parameter | Type | Description
--------- | ---- | -----------
revokedGoods | JSON | The map of revoked goods
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
transactionIds | REQUIRED | The transactionIds is missing
storeType | REQUIRED | The storeType is missing
playerId | REQUIRED | The playerId is missing

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new RevokePurchaseGoodsRequest()
		.SetPlayerId(playerId)
		.SetStoreType(storeType)
		.SetTransactionIds(transactionIds)
		.Send((response) => {
		GSData revokedGoods = response.RevokedGoods; 
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
	    .createRevokePurchaseGoodsRequest()
		.setPlayerId(playerId)
		.setStoreType(storeType)
		.setTransactionIds(transactionIds)
		.send(function(response:com.gamesparks.api.responses.RevokePurchaseGoodsResponse):void {
		var revokedGoods:Object = response.getRevokedGoods(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSRevokePurchaseGoodsRequest* request = [[GSRevokePurchaseGoodsRequest alloc] init];
	[request setPlayerId:playerId;
	[request setStoreType:storeType;
	[request setTransactionIds:transactionIds;
	[request setCallback:^ (GSRevokePurchaseGoodsResponse* response) {
	NSDictionary* revokedGoods = [response getRevokedGoods]; 
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
	
	void RevokePurchaseGoodsRequest_Response(GS& gsInstance, const RevokePurchaseGoodsResponse& response) {
	GSData revokedGoods = response.getRevokedGoods(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	RevokePurchaseGoodsRequest request(gsInstance);
	request.SetPlayerId(playerId)
	request.SetStoreType(storeType)
	request.SetTransactionIds(transactionIds)
	request.Send(RevokePurchaseGoodsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.RevokePurchaseGoodsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.RevokePurchaseGoodsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createRevokePurchaseGoodsRequest()
	.setPlayerId(playerId)
	.setStoreType(storeType)
	.setTransactionIds(transactionIds)
	.send(new GSEventListener<RevokePurchaseGoodsResponse>() {
		@Override
		public void onEvent(RevokePurchaseGoodsResponse response) {
			GSData revokedGoods = response.getRevokedGoods(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.RevokePurchaseGoodsRequest();
	request.playerId = ...;
	request.storeType = ...;
	request.transactionIds = ...;
	var response = request.Send();
	
var revokedGoods = response.revokedGoods; 
var scriptData = response.scriptData; 
```


