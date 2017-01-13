---
src: /API Documentation/Realtime API/RTPacketBuilder.md
---

# RTPacketBuilder

A builder object to construct RTPacket objects


## send
_signature_ send()</p>
_returns_ void</p>
Sends this packet to the current session with the given parameters

## setData
_signature_ setData([RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md) rtData)</p>
_returns_ [RTPacketBuilder](/API Documentation/Realtime API/RTPacketBuilder.md)</p>
Sets the RTData of the packet

## setOpCode
_signature_ setOpCode(number opCode)</p>
_returns_ [RTPacketBuilder](/API Documentation/Realtime API/RTPacketBuilder.md)</p>
Sets the opCode of the sent packet. Server sent packets will be send with opCode 0 if this is not set

## setReliable
_signature_ setReliable(boolean reliable)</p>
_returns_ [RTPacketBuilder](/API Documentation/Realtime API/RTPacketBuilder.md)</p>
Sets the packet to be sent as reliable. By default, server sent packets are sent as unreliable

## setSender
_signature_ setSender(number peerId)</p>
_returns_ [RTPacketBuilder](/API Documentation/Realtime API/RTPacketBuilder.md)</p>
Sets the peerId of the sent packet. Server sent packets will be send with peerId 0 if this is not set

## setTargetPeers
_signature_ setTargetPeers(Integer[] peerIds)</p>
_returns_ [RTPacketBuilder](/API Documentation/Realtime API/RTPacketBuilder.md)</p>
Sets the peer id's to send the packet to

