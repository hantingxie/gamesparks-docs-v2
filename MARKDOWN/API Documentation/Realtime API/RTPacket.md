---
src: /API Documentation/Realtime API/RTPacket.md
---

# RTPacket

An object representing a packet sent by a client


## getData
_signature_ getData()</p>
_returns_ [RTData](/API Documentation/Realtime API/RTData.md)</p>
Gets the RTData sent with the packet (if available)

## getSender
_signature_ getSender()</p>
_returns_ [RTPlayer](/API Documentation/Realtime API/RTPlayer.md)</p>
Gets the player who sent the packet

## getTargetPlayers
_signature_ getTargetPlayers()</p>
_returns_ number[]</p>
Gets the list of peerIds that this packet is being sent to. If this is empty the packet is targetting everyone except the sender 

