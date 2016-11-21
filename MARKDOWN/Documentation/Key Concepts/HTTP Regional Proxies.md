---
nav_sort: 8
src: /Documentation/Key Concepts/HTTP Regional Proxies.md
---

# HTTP Requests Routed via Regional Proxies

All outbound HTTP Requests originating from the GameSparks platform, such as *Spark.getHttp()*, are routed through our regional proxies.

## Regional Proxies

The following table lists our regional proxy servers and their IP addresses:

Region  | IP Address
-----  | -----------
Europe West   | 52.19.117.135
Europe West  | 52.18.101.45
US West  | 52.88.71.26
US West   | 52.88.148.140
US West   | 137.117.17.204
US West   | 40.78.70.195
China North   | 54.222.135.29
China North   | 54.222.144.141
Asia East   | 168.63.205.150
Asia East  | 52.175.22.165

## Whitelisting Traffic

Since all outgoing HTTP requests from the platform are routed through these proxies, you can whitelist calls to 3rd-party services to suit your specific needs.
