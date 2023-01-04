# Using Google Auth

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

POST `{{api-root-url}}/directory/api/users/google/auth`

```json
{
  "token": "899eddde2c5a16df72264c4116f3e351899eddde99eddde2c5a16df72264c4116f3e351899eddde",
}
```
