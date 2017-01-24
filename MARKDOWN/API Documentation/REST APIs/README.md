---
src: /API Documentation/REST APIs/README.md

---

# REST APIs Overview

## Usage
The GameSparks API is a RESTful API that can be used to access authentication, game administration and configuration, NoSQL, and service requests:
* [Authentication](/API Documentation/REST APIs/Authentication.md)
* [Game Administration](/API Documentation/REST APIs/Game Admin.md)
* [Game Configuration](/API Documentation/REST APIs/Game Configuration.md)
* [NoSQL](/API Documentation/REST APIs/NoSQL.md)
* [Service Requests](/API Documentation/REST APIs/Requests.md)

## Schema

* All API access is over HTTPS, and accessed from the https://portal.gamesparks.net for game management and https://apiKey.{stage}.gamesparks.net for service server.
* All data is sent and received as JSON.
* All dates and timestamps are returned in ISO 8601 format:

```

YYYY-MM-DD and YYYY-MM-DDTHH:MM:SSZ

```

## Authentication
Authentication is performed using Basic Authentication (with your portal credentials).

## HTTP Verbs

Verbs  | Description
-----  | -----------
GET    | Used for retrieving resources.
POST   | Used for creating resources.
PUT    | Used for updating resources.
DELETE | Used for deleting resources.

## Status Code

Code | Description
-- | --
200 | OK
201 | Created
401 | Unauthorized
403 | Not allowed
404 | Not found
420 | JSON error

## Examples
Event GET /restv2/game/{apiKey}/config/~events/{eventId}
Response example:
```
{
  "@id": "/~events/e1",
  "description": "e1_desc",
  "name": "e1_nam",
  "shortCode": "e1",
  "~attributes": []
}
```

Event POST /restv2/game/{apiKey}/config/~events example:
```
{
  "shortCode": "e2",
  "name": "e2_name",
  "description": "e2_desc"
}
```
Client error response example:
```
{
  "message": "Game not owned by current user"
}
```
