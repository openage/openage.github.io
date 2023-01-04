## Rule Action

Action can be of type `condition` which would be handled by condition handler

On an event, Composer executes set of actions. There are different types of action


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

	},
	"success": {
		"action": "b"
	},
	"failure": {
		"action": "c"
	}
}
```


```JSON
{            
	"code" : "a",
	"handler" : "http",
	"config" : {
		"source" : {
			"type" : "data"
		},
		"target" : {
			"url" : ":mo/particulars/${rootSource.particular}",
			"action" : "get",
			"headers" : {
				"Content-Type" : "application/json",
				"x-role-key" : "${context.user.role.key}"
			}
		}
	},
	"next": {
		"action": "is"
	}
}
```


```JSON
{
    "code" : "directory|employee|update",
    "name" : "On Employee Change",
    "status" : "active",
    "trigger" : "create",
    "dataSource" : {
        "params" : [],
        "type" : "http",
        "connectionString" : ":directory/employees/{{data.input.entity.code}}",
        "config" : {
            "headers" : {
                "x-role-key" : "{{context.user.role.key}}"
            }
        },
        "field" : "data",
        "key" : "rootSource"
    },
    "actions" : [ {
		    "code" : "is-transit",
		    "handler" : "decision",
		    "config": {
				"condition": {
					"key": "impex",
					"operator": "=",
					"value": "export"
				},
				"success": {
					"action": ""
				},
				"failure": {
					"action": ""
				}
		    }  
	    },
        {            
	        "code" : "get-tranist-particular",
            "handler" : "http",
            "config" : {
                "source" : {
                    "type" : "data"
                },
                "target" : {
                    "url" : ":mo/particulars/${rootSource.particular}",
                    "action" : "get",
                    "headers" : {
                        "Content-Type" : "application/json",
                        "x-role-key" : "${context.user.role.key}"
                    }
                }
            }
        }, 
        {
            "code" : "get-tranist-journey",
            "handler" : "http",
            "config" : {
                "source" : {
                    "type" : "data"
                },
                "target" : {
                    "url" : ":mo/journies/${rootSource.journey}",
                    "action" : "get",
                    "headers" : {
                        "Content-Type" : "application/json",
                        "x-role-key" : "${context.user.role.key}"
                    }
                }
            }
        }, 
        {
            "code" : "get-journey-order",
            "handler" : "http",
            "config" : {
                "source" : {
                    "type" : "data"
                },
                "target" : {
                    "url" : ":mo/orders/${get-tranist-journey.order.code}",
                    "action" : "get",
                    "headers" : {
                        "Content-Type" : "application/json",
                        "x-role-key" : "${context.user.role.key}"
                    }
                }
            }
        }, 
        {
            "code" : "update-customer-warehouse",
            "handler" : "warehouse",
            "config" : {
                "source" : {
                    "type" : "data"
                },
                "target" : {
                    "provider" : "insightdb",
                    "where" : {
                        "type" : "customer",
                        "code" : "{{get-journey-order.customer.code}}"
                    },
                    "create" : {
                        "type" : "customer",
                        "code" : "{{get-journey-order.customer.code}}"
                    },
                    "update" : {
                        "list" : "data.orders",
                        "mapping" : {
                            "code" : "get-journey-order.code",
                            "oceanTranitStatus" : "get-tranist-journey.status",
                            "carrier_code" : "get-tranist-particular.rate.supplier.code",
                            "carrier_name" : "get-tranist-particular.rate.supplier.name"
                        },
                        "where" : {
                            "operator" : "AND",
                            "value" : [ 
                                {
                                    "key" : "code",
                                    "operator" : "==",
                                    "value" : "{{get-journey-order.code}}"
                                }
                            ]
                        }
                    }
                }
            }
        }, 
        {
            "code" : "update-container",
            "handler" : "warehouse",
            "config" : {
                "target" : {
                    "provider" : "insightdb",
                    "where" : {
                        "type" : "container",
                        "data.container.order" : "{{get-journey-order.code}}"
                    },
                    "update" : {
                        "mapping" : {
                            "carrier_code" : "get-tranist-particular.rate.supplier.code",
                            "carrier" : "get-tranist-particular.rate.supplier.name",
                            "trackingCurrentStatus" : "rootSource.tracking.currentStatus",
                            "transitType" : "rootSource.type",
                            "vessel" : "rootSource.vessel",
                            "trackingCurrentLocCode" : "rootSource.tracking.trackingCurrentLocCode"
                        },
                        "field" : "data.container"
                    }
                }
            }
        }
    ]

}

```


#composer #rules #action #condition