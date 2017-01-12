# RTDataBuilder

A builder object to construct RTData objects


## setData
_signature_ setData(number index, [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md) value)</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Adds a nested RTData object at the given index key

## setDouble
_signature_ setDouble(number index, Number value)</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Adds a double at the given index key, the number will be added as a protobuf fixed64

## setFloat
_signature_ setFloat(number index, Number value)</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Adds a float at the given index key, the number will be added as a protobuf fixed32

## setFloatArray
_signature_ setFloatArray(number index, Number[] values)</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Adds a an array of floats at the given index key

## setNumber
_signature_ setNumber(number index, Number value)</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Adds a number at the given index key, the number will be added as a protobuf varint

## setString
_signature_ setString(number index, string value)</p>
_returns_ [RTDataBuilder](/API Documentation/Realtime API/RTDataBuilder.md)</p>
Adds a string at the given index key

