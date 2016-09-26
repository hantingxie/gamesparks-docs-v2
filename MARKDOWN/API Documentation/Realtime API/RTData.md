---
src: /API Documentation/Realtime API/RTData.md
---

# RTData

The javascript representation of an RTData object

This object allows you to inpect the RTData objects sent from a client

This object is immutable, to create a new one you should use RTSession.getRTDataBuilder()


## getData
_signature_ getData(number index)</p>
_returns_ [RTData](/API Documentation/Realtime API/RTData.md)</p>
Gets an RTData object using the given index key, if the key contains a different type, or is empty a null will be returned

## getDouble
_signature_ getDouble(number index)</p>
_returns_ number</p>
Gets a double using the given index key, if the key contains a different type, or is empty a null will be returned

## getFloat
_signature_ getFloat(number index)</p>
_returns_ Float</p>
Gets a float using the given index key, if the key contains a different type, or is empty a null will be returned

## getFloatArray
_signature_ getFloatArray(number index)</p>
_returns_ Float[]</p>
Gets a float array using the given index key, if the key contains a different type, or is empty a null will be returned

## getNumber
_signature_ getNumber(number index)</p>
_returns_ number</p>
Gets a number using the given index key, if the key contains a different type, or is empty a null will be returned

## getString
_signature_ getString(number index)</p>
_returns_ string</p>
Gets a string using the given index key, if the key contains a different type, or is empty a null will be returned

