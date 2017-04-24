---
nav_sort: 6
src: /Tutorials/Game Engine Integrations/Using SetDurable in Java.md
---

# Java Setting Durable Requests

If requests are sent without being set as durable while the device isn't connected to GameSparks due to connection problems they will timeout. If those requests were set to durable before being sent off, they will be queued and resent once the device regains connection to the backend.

<q>**Using the SetDurable Parameter?** For more details on how and when to use the SetDurable parameter, see [here](/Tutorials/Game Engine Integrations/Using the SetDurable Parameter.md).</q>

To set a request as durable in Java you'll need to instantiate the request first, then set it as durable. This is because the *setDurable* method does not return the request.

Here's how to instantiate and set a request as durable:

*1.* Import the request that you're instantiating. For our example we're instantiating a [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md):

```
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.LogEventRequest;

```

*2.* Instantiate the request:

```
LogEventRequest req = GSAndroidPlatform.gs().getRequestBuilder().createLogEventRequest();

```

*3.* Set durable true:

```
req.setDurable(true);
```

*4.* Send the request:

```
req.send(new GSEventConsumer<GSResponseBuilder.LogEventResponse>() {
            @Override
            public void onEvent(GSResponseBuilder.LogEventResponse logEventResponse) {

            }
        });
```

This can be done for every request in the GameSparks API library.
