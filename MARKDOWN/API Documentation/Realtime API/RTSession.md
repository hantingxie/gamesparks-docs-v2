# RTSession

The main entry point into the GameSparksRT API


## clearInterval
_signature_ clearInterval(Number intervalId)</p>
_returns_ void</p>
Clears an interval using the id returned from a previous setInterval call

## clearTimeout
_signature_ clearTimeout(Number timeoutId)</p>
_returns_ void</p>
Clears a timeout using the id returned from a previous setTimeout call

## getLogger
_signature_ getLogger()</p>
_returns_ [RTLogger](/API Documentation/Realtime API/RTLogger.md)</p>
Gets the logger object. Log records are written to the GameSparks collection " realtime.log"

## newData
_signature_ newData()</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Creates a new builder object to construct RTData objects

## newPacket
_signature_ newPacket()</p>
_returns_ [RTPacketBuilder](/API Documentation/Realtime API/RTPacketBuilder.md)</p>
Creates a new builder object to construct RTPacket objects

## newRequest
_signature_ newRequest()</p>
_returns_ RTRequestBuilder</p>
A builder object for creating and sending requests to the GameSparks platform

## onPacket
_signature_ onPacket(number opCode, fn(packet: RTPacket) paramName)</p>
_returns_ void</p>
Register a callback to be invoked when a packet with the given opCode is recieved. If this function does not return the supplied packet, the packet will not be sent to any players

## onPlayerConnect
_signature_ onPlayerConnect(fn(player: RTPlayer) paramName)</p>
_returns_ void</p>
Register a callback to be invoked when a player connects to the session

## onPlayerDisconnect
_signature_ onPlayerDisconnect(fn(player: RTPlayer) paramName)</p>
_returns_ void</p>
Register a callback to be invoked when a player disconnects from the session

## getPlayer
_signature_ getPlayer(number peerId)</p>
_returns_ [RTPlayer](/API Documentation/Realtime API/RTPlayer.md)</p>
Gets a player by peerId

## getPlayers
_signature_ getPlayers()</p>
_returns_ [RTPlayer](/API Documentation/Realtime API/RTPlayer.md)[]</p>
Gets all connected players

## getSessionId
_signature_ getSessionId()</p>
_returns_ string</p>
Gets the current sessionId

## setInterval
_signature_ setInterval(fn() paramName, number ms)</p>
_returns_ Number</p>
The setInterval() method calls a function or evaluates an expression at specified intervals (in milliseconds).
The setInterval() method will continue calling the function until clearInterval() is called, or the window is closed
The ID value returned by setInterval() is used as the parameter for the clearInterval() method.

## setTimeout
_signature_ setTimeout(fn() paramName, number ms)</p>
_returns_ Number</p>
Calls a function or evaluates an expression after a specified number of milliseconds.

