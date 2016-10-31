---
nav_sort: 5
src: /Tutorials/Social Authentication and Player Profile/Using Bulk Operations for Global Messages.md
---

# Using Bulk Operations to Send Global Messages to Players

The GameSparks platform allows you to perform bulk operations. In this tutorial, we’ll use bulk operations to send every player on our platform a message. There are two ways to do this:
* Through the request itself.
* Through Cloud Code.

## Sending Global Messages through the Request

Here, we use a [ScheduleBulkJobAdminRequest](/API Documentation/Request API/Admin/ScheduleBulkJobAdminRequest.md) to send a global message to players through the Test Harness:

```

{
 "@class": ".ScheduleBulkJobAdminRequest",
 "playerQuery": {},
 "scheduledTime": "2016-03-29T10:16Z",
 "script": "Spark.sendMessageById({\"Message\": \"Good day!\"}, [Spark.getPlayer().getPlayerId()]);"
}

```

You'll need to set three fields:

* *playerQuery* – Takes a query that acts on the player database Collection. This can be anything relevant to the player document found in the player Collection.
* *scheduledTime* – The time when this bulk job should take place.
* *script* – The Cloud Code that will execute on every player.

Note that in this example:
* Because we have left playerQuery blank, all players will be included in this bulk job.
* We've used Cloud Code to define the text of the message players will receive.
  * Due to the request taking the script in as a string, Cloud Code with quotes will cause problems in the compiler and hence it will not run. So here we use an escape character ‘\’ before a quotation to allow us to carry on.

### Using a Module in the Request

Another way to use the *ScheduleBulkJobAdminRequest* to send a global message to your players is to execute a module by referring to its Short Code:


```

{
 "@class": ".ScheduleBulkJobAdminRequest",
 "moduleShortCode": "messageModule",
 "playerQuery": {},
 "scheduledTime": "2016-03-29T10:32Z"
}

```

In this example, when the request is executed, every player will be sent the message set in the module.

<q>**Using Modules?** Modules allow you to create your own libraries of JavaScript that can be included within other scripts. For more details see the *Modules* section in [Cloud Code](/Documentation/Configurator/Cloud Code.md)</q>

## Sending Global Messages through Cloud Code

You can send a bulk job request in Cloud Code in two ways:
* Building a bulk job via request builder.
* Sending it via Spark.sendRequest.

### Building Bulk Job via Request Builder

```

var bulkJobRequest = new SparkRequests.ScheduleBulkJobAdminRequest();

//If using module
bulkJobRequest.moduleShortCode = "messageModule";

//If using script
bulkJobRequest.script = "Spark.sendMessageById({\"Message\": \"Good day!\"}, [Spark.getPlayer().getPlayerId()]);";

bulkJobRequest.scheduledTime = "2016-03-29T10:32Z";

bulkJobRequest.playerQuery = {};

bulkJobRequest.Send();


```

### Sending Bulk Job via Spark.sendRequest

```

Spark.sendRequest({"@class": ".ScheduleBulkJobAdminRequest",
 "playerQuery": {},
 "scheduledTime": "2016-03-29T10:16Z",
 "script": "Spark.sendMessageById({\"Message\": \"Good day!\"}, [Spark.getPlayer().getPlayerId()]);"});


```
