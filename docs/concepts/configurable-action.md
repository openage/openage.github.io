# Configurable Action

Attribute of an action
- Code
- Handler
	- navigate
	- button
	- form
	- workflow
	- api/backend (used by services)
- Title
- Permissions
- View and Type are used to render the UI
- Config - is handler specific
- 

## UI Actions

UI actions are rendered using `oa-action`. Here are sample actions

### Navigate action

```JSON
{
	"code": "navigate",
	"handler": "navigate",
	"view": "button", // (was type)
	"title": "Activate",
	"config": {
		"url": "/master/customers/:code"
	}
}
```


### Reload action

```JSON
{
	"code": "refresh",
	"handler": "reload",
	"view": "button", // (was type)
	"title": "Reload",
	"config": {	
	}
}
```


### Phone Verification action

```JSON
{
	"code": "abc",
	"handler": "login",
	"view": "button", // (was type)
	"title": "Login",
	"config": {	
	}
}
```


### Login action

```JSON
{
	"code": "abc",
	"handler": "login",
	"view": "button", // (was type)
	"title": "Login",
	"config": {	
	}
}
```


### Logout action

```JSON
{
	"code": "abc",
	"handler": "logout",
	"view": "button", // (was type)
	"title": "Login Again",
	"config": {	
	}
}
```

### Form action

In notifications - the form will be shown as collapsed, with button having `title` 

In case of error - the form shoule be shown in expanded form.
```JSON
{
	"code": "",
	"handler": "form",
	"title": "Add Missing Data",
	"view": "object-editor", // (was type)
	"order": 1, // sequence
	"permissions": ["operator"],
	"config": {
		"collapesed": true,
		"fields": [{
		}],
		"target" : {
			"type": "http",
			"url" : ":mo/bookings/${data.code}",
			"action" : "put",
		}
	}
}
```

### View action
```JSON
{
	"code": "",
	"handler": "view",
	"view": "object-viewer", // (was type)
	"title": "BL Details",
	"config": {
		"fields": [{
		}],
		"source" : {
			"type": "http",
			"url" : ":mo/booking?order-code${data.code}",
			"action" : "get",
		}
	}
}
```

### Workflow Action
```JSON
{
	"code": "activate-customer",
	"handler": "workflow",
	"config": {	
		"source": {
			"type": "http",
			"url" : ":gateway/tasks/customer-onboarding:customer:${data.code}",
			"action" : "get"
		}
	}
}
```



### Notify Action

```JSON
{
	"code": "notify-admin",
	"handler": "message-composer",
	"config": {	
		"template": "admin-message",
		"target": {
			"type": "http",
			"url" : ":send-it/messages",
			"action" : "post"
		}
	}
}
```


### Decision Action
```JSON
{
	"code" : "is",
	"handler" : "decision",
	"config": {
		"condition": {
			"key": "impex",
			"operator": "=",
			"value": "export"
		},
		"success": {
			"action": "b"
		},
		"failure": {
			"action": "c"
		}
	},
	
}
```


TODO: unify the data injector
- Service url injection
- Parameter (body/query) injection
- Header Injection