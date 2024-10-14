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

In case of error - the form should be shown in expanded form.
```JSON
{
	"code": "reset",
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

### Vie

In notifications - the form will be shown as collapsed, with button having `title` 

In case of error - the form should be shown in expanded form.
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

### Application Action
#process-action 

#### Scrapping Action
#scrapper 
```JSON
{
	"code": "get-rates-from-vendor-site",
	"application": {
		"code": "dex"
	},
	"handler": "scrapper",
	"config": {	
		"source": {
			"type": "web-view",
			"url": "https://www.msc.com/en/search-a-schedule",
			"action" : "load"
		},
	    "steps": [
	        {
	            "code": "initialize-page",
	            "actions": [
	                {
	                    "type": "navigate",
	                    "url": "[https://www.msc.com/en/search-a-schedule](https://www.msc.com/en/search-a-schedule)",
	                },
	                // {
	                //     "type": "click",
	                //     "path": "#onetrust-reject-all-handler",
	                // },
	            ],
	        },
	        {
	            "code": "set-port",
	            "actions": [
	                {
	                    "type": "set",
	                    "path": "#from",
	                    "value": "mundra",
	                },
	                {
	                    "type": "wait",
	                    "path": ".msc-search-schedule__input--from > .msc-search-schedule__autocomplete > ul > li:nth-child(4) > .port",
	                },
	                {
	                    "type": "click",
	                    "path": ".msc-search-schedule__input--from > .msc-search-schedule__autocomplete > ul > li:nth-child(4) > .port",
	                },
	                {
	                    "type": "to",
	                    "path": "#from",
	                    "value": "hamburg",
	                },
	                {
	                    "type": "wait",
	                    "path": "todo",
	                },
	                {
	                    "type": "click",
	                    "path": ".msc-search-schedule__input--to > .msc-search-schedule__autocomplete > ul > li:nth-child(4) > .port",
	                },
	                {
	                    "path": "#submit",
	                    "value": "click",
	                    "selector":
	                        ".grid-x > .cell > .msc-search-schedule__form:nth-child(2) > .msc-search-schedule__submit > .msc-cta",
	                },
	            ],
	            //   "gather": [
	            //     {
	            //       "path": "msc-search-schedule-result-details__result",
	            //       key: "schedule-list",
	            //       className: "msc-search-schedule-result-details__result",
	            //     },
	            //   ],
	            //   build: [
	            //     {
	            //       field: "source-port",
	            //       key: "source-port-code",
	            //     },
	            //     {
	            //       field: "destination-port",
	            //       key: "destination-port-code",
	            //     },
	            //   ],
	            // },
	            // ],
	        },
	    ],
		"target": {
			"type": "http",
			"url" : ":rates/price",
			"action" : "post"
		}
	}
}
```

#### File Action
#file #sync #download 

```JSON
{
	"code": "pull-files",
	"application": {
		"code": "dex"
	},
	"handler": "file-sync",
	"config": {
		"source": {
			"type": "http",
			"url": ":drive/files/xxxxxxxxx"
		},
		"target": {
			"type": "path",
			"path": "customers/cust-1/pan-card.png"
		}
	}
}
```

#upload #file #sync
```JSON
{
	"code": "push-updated-files",
	"application": {
		"code": "dex"
	},
	"handler": "file-sync",
	"config": {
		"source": {
			"type": "path",
			"path": "customers/cust-1/pan-card.png"
		},
		"target": {
			"type": "http",
			"url": ":drive/files/xxxxxxxxx?folder-code=cust-1&entity-type=customer"
		}
	}
}
```

#open #file
```JSON
{
	"code": "open-file",
	"application": {
		"code": "dex"
	},
	// need ability to target a specific instance of the app
	"handler": "file-run", // file-print
	"config": {
		"source": {
			"type": "path",
			"path": "customers/cust-1/pan-card.png"
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


#todo : unify the data injector
- Service url injection
- Parameter (body/query) injection
- Header Injection