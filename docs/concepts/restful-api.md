
# RESTful API

## URL convention
Resource Url `{{api-root-url}}/{{service-code}}/api/v1/{{resource}}`. It has following parts

1. `api-root-url` - the hosting url of the API, e.g. `https://api.app-domain.com`
2. `service-code` - the code with which the service has been registered with the framework
3. `v1` - version of the service, by default it would not present
4. `resource` - the collection, e.g. `sessions`, `users`, `organizations` etc

## List of resources
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

### Searching
You can pass query parameters to search by properties. 

### Paging
In addition you should can implement paging by using `limit` and `offset` query params.

### Sorting
You can pass primary sort in query params as `sort=field-name` and `desc=true` for direction of the sort.

### Creating a new resource
A new resouce can be creating by using `POST` operation with model in the body.

## Single Resource

To Get the detailed resource using following
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

#### Operations on the resource
- `GET` to get a resource
- `PUT` to update a resource
- `DELETE` to remove a resource

## Expection Handing

### Generic Errors
In case an error occurs while processing the request, the server would return following HTTP Status
- `400` Acess denied
- `500` Unknown Error

### Validation Errors
In case an operation fails it wold return `HTTP Status = 200` but would in addition return 
```JSON
{
	"isSuccess": false,
	"code": "{ErrorCode}"
}
```

Error codes are 7 digits with the following breakup

1. 2 digit Service Identifier
1. 2 digit Action Identifier
1. 3 digit Error Identifier

`DI_SG_EXP` error, for example, would mean 
`DI` - Directory 
`SG` - Session Get 
`EXP` - Expired`

Service Identifiers

1. `CN` - Connect Service
1. `DI` - Directory Service
1. `SI` - SendIt Service
1. `DR` - Drive Service
1. `IN` - Insight Service
1. `VA` - Vault Service
1. `MP` - Composer Service
1. `GW` - Gateway Service
1. `BP` - Billing Service
1. `MO` - Operation Service
1. `RE` - Rates Service
1. `SA` - Sales Service