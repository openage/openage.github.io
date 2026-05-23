# Using Google Auth

#authentication #Custom #plugin

Step 1: Setup config in Tenant Config

```JSON
{
  "config": {
	  "auths" : [ 
            {
                "code" : "abc", // auth Code
                "url" : "url", // URL where to hit the request
                "type" : "POST", // Type of request
                "headers" : {},
                "req" : { // Request Body want to send and it will be injected by Query Params of the request
                    "loginID" : "${username}", 
                    "userPassword" : "${password}"
                },
                "res" : { // A Standard User object will be made from the response body (code | email | phone require to create user)
					"code" : "code", // To inject code ${res.code}, In res we have response body
                    "email" : "email", // To inject code ${res.email}, In res we have response body
                    "phone" : "phone", // To inject code ${res.phone}, In res we have response body
                    "profile" : {
                        "firstName" : "name",
						"lastName": "name",
          				"pic" : {
                			"url": "pic url"
           				}
                    }
                }
            }
        ]
  }
}
```

Step 2: Create and get the session

* **Url**: `{{api-root-url}}/directory/api/users/custom/auth/success`
* **Type**: POST
* **Params**:

We can add multiple Param and Add dynamically to the request body

```json
{
	"username": "username", // Add email | phone | anyother to add in request
	"password": "", // add password
	"code": "", // Required Add Tenant Auth Code
}
```

The directory will
* Validate the Auth Code
* Create dynamic request and Hit the Request 
* Mapp the reqponse to user Model
* Check and Create the user
* Create a active session

Here is the sample `session` object returned by the system:

**Response:**
```JSON
{
	"id": "605c47eec0b3c67843e85466",
	"purpose": "login",
    "app": "chrome",
    "expiry": "2021-03-25T08:21:02.104Z",
	"status": "active",
	"token": "1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY",
	"role": {
		"id": "605c47eec0b3c67843e85467",
		"key": "57605ffa-0ec4-a911-70c7-1edba4b70272",
		"code": "xxxxxxx",
		"permissions": ["organization.admin"],
		"type": {
			"id": "5fd4c92cb9ba1d02b98f8e2d",
			"code": "organization.admin",
			"name": "Organization Admin"
		},
		"employee": {},
		"organization": {},
		"status": "active"
	},
	"user": {
		"email": "user@organization.com",
		"profile": {},
		"meta": {
			"user": {} // Response which we get from the Custom hit API
		}		
	}
}
```