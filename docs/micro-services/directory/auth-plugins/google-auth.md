# Using Google AUTH

#authentication #google #plugin


Step 1: Get the token from google

Step 2: Create and get the session

Send following request to
* **Url**: `{{api-root-url}}/directory/api/sessions`
* **Type**: POST
* **Body**:

```JSON
{
    "purpose": "login",
    "app": "chrome",
    "auth": "google",
    "user": {
        "email": "admin@organization.com",
        "google-token": "899eddde2c5a16df72264c4116f3e351899eddde99eddde2c5a16df72264c4116f3e351899eddde"
    }
}
```

The api would respond back with the session object.

Following mechanism is obsolete

* **Url**: `{{api-root-url}}/directory/api/users/google/auth/success`
* **Type**: POST
* **Params**:

```json
{
  "app": "chrome xsxsxsxsx", // App Code
  "code": "id_token"
}
```
The directory will
* Validate the token
* Validate the User
* If user does not exit it will create
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
		"profile": {}		
	}
}
```