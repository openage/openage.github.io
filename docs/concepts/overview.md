# Overview

List of services

## Key Mechanisms

#### RESTful API

Resource Url `{{api-root-url}}/{{service-code}}/api/v1/{{resource}}`. It has following parts

1. `api-root-url` - the hosting url of the API, e.g. `https://api.openage.in`
1. `service-code` - the code with which the service has been registered with the framework
1. `resource` - the collection, e.g. `sessions`, `users`, `organizations` etc

- To Get a list of resources `GET {{api-root-url}}/{{service-code}}/api/v1/{{resource}}?skip=50&limit=10&sort=date`. The list would be returned as `items` in _data_. e.g.

```JavaScript
{
    "isSuccess": true,
    "data": {
        "items": [{
            "id": "5fc03087-d265-11e7-b8c6-83e29cd24f4c",
            // ...
        }, {
            // ...
        }],
        "skip": 50,
        "limit": 10,
        "total": 52,
        "sort": "date"
        "desc": true
    }

}
```

- To Get the detailed resource using following
  - `GET {{api-root-url}}/{{service-code}}/api/v1/{{resource}}/{{id}}`
  - `GET {{api-root-url}}/{{service-code}}/api/v1/{{resource}}/{{code}}`

The resource will be available as `data` of the response would get you following response.

```JavaScript
{
    "isSuccess": true,
    "data": {
        "id": "5fc03087-d265-11e7-b8c6-83e29cd24f4c",
        // ...
    }
}
```

To access secured resources the request header needs to have the bearer token `x-access-token`

In addition, the request would have `context-id` in _header_.  It would be passed to subsequent calls to bind the logs across services/components into a single request


### Errors

HTTP Status

Validation Errors


Error codes are 7 digits with the following breakup

1. 2 digit Service Identifier
1. 2 digit Action Identifier
1. 3 digit Error Identifier

`DISGEXP`, for example, can be broken down to `DI SG EXP` and would mean `DIrectory Session Get EXPired`

Service Identifiers

1. DI - Directory Service
1. DV - Discovery Service
1. 
1. SI - SendIt Service
1. DR - Drive Service
1. GW - Gateway Service
1. IN - Insight Service
1. BP - Billing Service
1. MO - Operation Service
1. SL - Sales Service