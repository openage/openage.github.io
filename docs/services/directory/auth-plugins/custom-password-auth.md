# Custom Auth Source
#authentication #custom #plugin

In case an API exists that can authenticate a user using its user id and password. To use that API, we need to do following.

1. Make the directory aware of the new auth mechanism
2. Configure your payload to get the session using the [login](/services/directory/session-login.md) mechanism

## Configuring the Custom API

You need to add following object to the directory configuration `config.auth.custom`

```JSON
{
	"code": "erp",
	"name": "Legacy Auth",
	"handler" : "http",
	"config": {
		"seed": true,
		"req": {
			"url" : "legacy-root/login",
			"action" : "POST",
			"headers" : {
				"Content-Type" : "application/json"
			},
			"mapper": [{
				"key": "employeeId",
				"value": "user.employee.code" // assuming the response comes as data.api_token
			}, {
				"key": "password",
				"value": "user.password"
			}]
		},
		"res": {
			"mapper": [{
				"key": "token",
				"value": "api_token" // assuming the response comes as data.api_token
			}, {
				"key": "expiry",
				"value": "token_expiry"
			}, {
				"key": "user.role.permissions",
				"value": "user_permissions"
			}]
		}
	}
}
```

The handler will send the request to `config.req.url` and the payload of the request would be mapped based on the `cofig.req.mapper`. For example for the above configuration the payload from the UI would be following

```JSON
{
   "purpose": "login",
   "app": "chrome",
   "auth": "custom",
   "user": {
	   "employee": {
		   "code": "SS-29"
	   },
       "password": "123123"
   }
}
```

and the request created for the custom auth would be 
```JSON
{
   "purpose": "login",
   "app": "chrome",
   "auth": "custom",
   "user": {
	   "employee": {
		   "code": "SS-29"
	   },
       "password": "123123"
   }
}
```

the response would be remapped to session object using the `config.res.mapper` values. 

The session object would be stored in the `sessions` db. 

If the user does not exist and the `config.seed = true` then the `user` and `role` would created and saved in the db. 

You can extend the session object using the mapper config.

## Sending Authenticating Request

`POST` the session create request to  `{{api-root-url}}/directory/api/sessions`  in following format

```JSON
{
   "purpose": "login",
   "app": "chrome",
   "auth": "custom",
   "user": {
       "email": "admin@organization.com",
       "password": "123123"
   }
}
```

