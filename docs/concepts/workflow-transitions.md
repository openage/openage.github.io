# Workflow Transitions

```JSON
{
	"code": "a",
	"transitions": [{
		"code": "a-to-b",
		"label": "Start",
		"rules":[{
			"handler": "conditions"
		}, {
			"handler": "security"
		}],
		"action": { 
			"handler": "composer",
			"config": {
				"code": "gateway"
			}
		}, // composer task code
		"isAuto": false, 
		"stage": {
			"code": "b"
		}
		
	}, {
		"code": "a-to-c",
		"label": "Pause",
		"rules":[{
			"type": "conditions"
		}, {
			"type": "security"
		}],
		"isAuto": false, 
		"stage": {
			"code": "c"
		}
		
	}]
}
```