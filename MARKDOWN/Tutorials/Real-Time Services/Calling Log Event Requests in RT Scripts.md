---
nav_sort: 9
src: /Tutorials/Real-Time Services/Calling Log Event Requests in RT Scripts.md
---

# Calling Log Event Requests in RT Scripts

A [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md) has attributes that don't work exactly like *scriptData*. You need a way to include the *scriptData* in the request. This tutorial provides an example that demonstrates how to include *scriptData* in a *LogEventRequest*.

<q>**LogChallengeEventRequests** The following applies equally to calling *LogChallengeEventRequest* from RT scripts.</q>

For the example, we'll create an Event with two Attributes:

* *testvar* of type string
* *testvar2* of type JSON

## Setting Event Attributes

Here's how we can set these Attributes for our log event:

```
var request = RTSession.newRequest()
        .createLogEventRequest()
        .setEventKey("event");
    request.settestvar("Hey this is a string");
    request.settestvar2({"key":"value"});
    request.setPlayerId(packet.getSender().getPlayerId())
        .send(function(response){
            RTSession.getLogger().debug(response);
        });

```

## Understanding the JSON Constructor:

* The JSON constructor looks for the word *set*. When it finds an instance of *set*, it creates a *key* which is equal to the string appended to *set*.
* The value given in brackets is then paired with this *key* as the *value* for the *key*.
* In the above code block we see some examples of the JSON Constructor at work:
  * .setEventKey("event") give us the *key/value* JSON pair {"eventKey":"event"}
  * .settestvar("Hey this is a string") give us the *key/value* JSON pair {"testvar":"Hey this is a string"}

So, our above code block for setting the Event Attributes will be unpacked into the following JSON:

```
{"eventKey:"event",testvar:"Hey this is a string",{"testvar2":{"key":"value"}},"playerId":"playerId"};

```

## Formatting Constraints

When using *set* in these sorts of case, the first character after an instance of *set* will *always be rendered* as lower case:
* For example, if your Attribute is named "ATTRIBUTE" it will be rendered as: "aTTRIBUTE".
