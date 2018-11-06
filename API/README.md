# Notes for API engineering

## RPC vs REST

RPC (**Command-based**) style endpoints are great when you want only one job done well. This makes it useful to one or two app clients because it is niche a service. RPC endpoints can implement business logic inside the service, given that it only does one thing. This adds simplicity and clarity to the service.

```HTTP
GET /someoperation?data=anId

POST /anotheroperation
{
  "data":"anId";
  "anotherdata":"another value"
}
```

For a REST (**resource-based**) endpoint, you must treat it like a resource that provides domain data. The reward is you are now segregating data into separate domains. This makes it useful for when you have any number of apps requesting data. This approach attempts to decouple data from application or business logic.

```HTTP
GET /someresources/anId

PUT /someresources/anId
{"anotherdata":"another value"
```
