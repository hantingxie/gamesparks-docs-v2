---
nav_sort: 2
src: /Documentation/Upgrading REST APIs/README.md
---

# Upgrading your REST APIs

GameSparks Portal2 introduced a new REST API. You must now upgrade to using our new REST API. This tutorial provides an overview of the new REST API and explains how to upgrade to it.

<q>**Read First!** Before going through this tutorial please read the REST API Overview [here](/API Documentation/REST APIs/README.md).</q>

<q>**Using NoSQL REST API?** If you are using the NoSQL REST API, then please also refer to this [tutorial](/API Documentation/NoSQL REST API.md) to help you with the upgrade process.</q>

## Old and New REST APIs

There are two old REST APIs:
* One available under: `https://portal.gamesparks.net`
* One available under: `https://config.gamesparks.net`

There is one new REST API:
* Available under: `https://config2.gamesparks.net`

## Understanding the New REST API

The important thing to note about the new REST API is that we've imposed a uniform structure in order to make it more comprehensive and extensible. Here are a few key features that you might notice when you start to work with it:
* Only two types of Content-Type headers are supported:
  * Application/json - used for the majority of the requests.
  * Multipart/form-data - used for requests that upload files.
* Each entity now has an address, represented by the “@id” key.
* Dependencies between entities are represented using the “@ref” key.
* By default, when you do a GET, only top-level entities are returned. In order to retrieve the entire game you can use the full=true parameter.
* Only the correct http verbs are used: GET, POST, PUT, PATCH, and DELETE.

## Upgrading from portal.gamesparks.net

<q>**Important: Restriction when Upgrading!** If you've obtained a JSON representation of the game from portal.gamesparks.net, this *cannot be* PUT back into the new REST API, because the structure is incompatible.</q>

Here's the steps to upgrade from this old REST API.

Use of GET:
* Replace:
  * GET `https://portal.gamesparks.net/rest/games/{apiKey}`
* With:
  * GET `https://config2.gamesparks.net/restv2/game/{apiKey}/config?full=true`

Use of POST:
* Replace:
  * POST `https://portal.gamesparks.net/rest/games/{apiKey}`
* With:
  * PUT `https://config2.gamesparks.net/restv2/game/{apiKey}/config`

## Upgrading from config.gamesparks.net

The new *config2.gamesparks.net* REST API extends the old *config.gamesparks.net* REST API and provides:
* Additional validations to safeguard data integrity.
* Wider functionality to support all portal operations.

Despite this continuity, going forward you should stop using the old REST API altogether and upgrade to the new API, because certain significant incompatibilities in data structure now exist between the old and new REST APIs.

To upgrade, and to avoid any disruptions that these incompatibilities of data structure may cause, follow this process:
* When you are ready to make changes to your game, perform a GET against *config2.gamesparks.net*, make the changes, and then perform a PUT back into *config2.gamesparks,net*.

<q>**Do Not Use Old and New APIs Interchangeably!** You should not attempt to GET your game from *config.gamesparks.net*, make your changes, and then PUT your game to *config2.gamesparks.net*.</q>

The new REST API is split into several individual applications, all as described in the [REST API Overview](/API Documentation/Rest APIs/README.md) page. Therefore, depending on what functional area you are using, you might need to split your calls between these endpoints:
* `https://auth.gamesparks.net` - Permission-related information.
* `https://config2.gamesparks.net` - Game and configuration-related information.
