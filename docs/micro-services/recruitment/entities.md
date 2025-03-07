# Recruitment Entities
#recruitment 

Stories Reference Design - 

(Open new Job position) https://app.actionitems.in/work/projects/at/tasks/at-29
(Job Listing) - https://app.actionitems.in/work/projects/at/tasks/at-30

Job
```JSON
{
	"code": String,
	"title": String,
	"description": String,
	"address": {
		"location": [] // cordinates
	},
	"type": Enum, // full time, consultant
	"keywords": [String],
	"skills": [{
		"type": Ref,
		"level": Number // begineer, experienced, expert
	}],
	"experience": {
		"min": Number,
		"max": Number
	},
	"salary": {
		"min": Number,
		"max": Number,
		"currency": String // INR, USD etc
	},
	"qualifications": {
		"min": String
	},
	"screenings": [{
		"type": Ref,
		"status": String,
		"user": Ref
	}],
	
	"organization": Ref,
	"tenant": Ref,
	"visibility": Number, // private, internal, public
	"status": String // draft, active, closed, rework, discarded
}
```

Candidate

Public Job listing Page - https://app.actionitems.in/work/projects/at/tasks/at-39
Job Applicant / Candidate - https://app.actionitems.in/work/projects/at/tasks/at-31



```JSON
{
	"profile": {
		"firstName": String,
		"lastName": String,
	},
	"address": {
		"location": [] // cordinates
	},
	"skills": [{
		"type": Ref,
		"level": Number // begineer, experienced, expert
	}],
	"qualifications": [Object],
	"expreience": [Object],
	"salary": {
		"current": Number,
		"expected": Number,
		"currency": String // INR, USD etc
	},
	"organization": Ref,
	
	"tenant": Ref,
	"status": "String" // draft, active, inactive, rework, discarded
}
```

Application

Job Applicant - https://app.actionitems.in/work/projects/at/tasks/at-31

```JSON
{
	"job": Ref,
	"candidate": Ref,
	"screenings": [{
		"type": Ref, // of round
		"date": Date,
		"summary": String, // high level comments
		"status": String, // unplanned, scheduled, result-awiated, passed, failed
		"user": Ref
	}],
	"organization": Ref,
	"tenant": Ref,
	"status": "String" // draft, submitted, active, in-progress, shortlisted, rejected, inactive, rework, discarded
}
```

Skills
```JSON
{
	"code": String,
	"name": String,
	"description": String,
	"category": String,
	"tenant": Ref
}
```

Rounds

Interview rounds Design - https://app.actionitems.in/work/projects/at/tasks/at-32

```JSON
{
	"code": String,
	"name": String,
	"duration": Number, // in minutes
	"type": Enum, // pre-screening, technical, HR etc
	"description": String, 
	"category": String,
	"organization": Ref,
	"tenant": Ref
}
```
