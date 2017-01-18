---
src: /API Documentation/Cloud Code API/Player/SparkPushRegistration.md
---

# SparkPushRegistration

The registration of a device to receive push notifications.
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var player = Spark.getPlayer().getPushRegistrations();</pre>


## getId

_signature_ getId()</p>
_returns_ string</p>

Gets the id of this registration.  This is the registrationId returned from the PushRegistrationResponse.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pushRegistration.getId();</pre>

## getPushId

_signature_ getPushId()</p>
_returns_ string</p>

Returns the id that uniquely identifies the device to the 3rd party push service.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pushRegistration.getPushId();</pre>

## getDeviceOS

_signature_ getDeviceOS()</p>
_returns_ string</p>

Returns the OS type for the device to which this registration belongs.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pushRegistration.getDeviceOS();</pre>
