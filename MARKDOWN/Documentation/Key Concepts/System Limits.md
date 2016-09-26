---
nav_sort: 7
src: /Documentation/Key Concepts/System Limits.md
---

# System Limits

The following limits are applied to the GameSparks API and Portal.

## Data Storage

Data Storage  | Limit | Resource Link
-----  | ----------- | -----
MongDB maximum document size    | Limit imposed by MongoDB. | [MongoDB Resource](https://docs.mongodb.com/manual/reference/limits/)

## Data Transfer

Data Transfer Type  | Limit
-----  | -----------
API Request    | 256KB
API Response   | 4MB
Downloadable asset   | 20MB
Uploadable asset    | maximum file size of 3.5MB
POST (REST API and NoSQL Explorer)    | 4MB
Packet Size    | 1400 bytes

## Concurrent Users - Preview only

No concurrency limit is applied to our Live API. Because Preview is only intended for development and internal testing purposes, the following limit is applied:

Concurrently Connected Users  | Limit
-----  | -----------
Live    | None
Preview   | 100
