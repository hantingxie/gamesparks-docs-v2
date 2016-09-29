# SparkMessage

Provides the ability to send a ScriptMessage and provide the configuration in code rather than from within the portal 


## setSendViaSocket
_signature_ setSendViaSocket(boolean value)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the Send Via Socket option.

## setSendAsPush
_signature_ setSendAsPush(boolean value)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the Send As Push option.

## setSupressPushOnSocketSend
_signature_ setSupressPushOnSocketSend(boolean value)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the Send As Push option.

## setIncludeInPushCount
_signature_ setIncludeInPushCount(boolean value)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the Include In Push Count option.

## setExpireAfterHours
_signature_ setExpireAfterHours(number hours)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the Time To Live (Hours) option.

## setDeviceTypes
_signature_ setDeviceTypes(string[] deviceTypes)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Limits the message delivery to only the device types supplied.

## setMessageData
_signature_ setMessageData(JSON data)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the data to send.

## setPlayerIds
_signature_ setPlayerIds(string[] playerIds)</p>
_returns_ [SparkMessage](/API Documentation/Cloud Code API/Player/SparkMessage.md)</p>

Sets the playerId to send the message to.

## send
_signature_ send()</p>
_returns_ void</p>

Sends the message.

