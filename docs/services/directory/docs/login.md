# Login

Login is achieved using session

## Using Password

Send following request to
* **Url**: `{{api-root-url}}/directory/api/sessions`
* **Type**: POST
* **Body**:

```JSON
{
   "purpose": "login",
   "app": "chrome",
   "user": {
       "email": "admin@organization.com",
       "password": "123123"
   }
}
```

Post session activation directory will add a `offline.queue('session', session, 'active', context)`
* For now there won't be any handler

**Response:**
```json
{
   "isSuccess": true,
   "data": {
        "id": "605c47eec0b3c67843e85466",
        "token": "1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY",
        "user": {
            "email": "admin@organization.com",
            "profile": {
                "firstName": "Organization",
                "lastName": "Admin",
                "pic": {
                    "url": "{{app-root-url}}/drive/files/605c67843e85466.png"
                }
            },
            "role": {
                "id": "605c47eec0b3c67843e85467",
                "key": "57605ffa-0ec4-a911-70c7-1edba4b70272",
                "code": "8805656713",
                "permissions": ["organization.admin"],
                "type": {
                    "id": "5fd4c92cb9ba1d02b98f8e2d",
                    "code": "organization.admin",
                    "name": "Organization Admin",
                    "status": "active",
                    "timeStamp": "2021-05-31T04:52:39.317Z"
                },
                "employee": {
                    "id": "305c47eec0b3c67843e85467",
                    "code": "1004",
                    "designation": {
                        "id": "395c47eec0b3c67843e85467",
                        "code": "admin",
                        "name": "Administrator"
                    },
                    "department": {
                        "id": "595c47eec0b3c67843e85467",
                        "code": "management",
                        "name": "Management"
                    }
                },
                "organization": {
                    "id": "705c47eec0b3c67843e85467",
                    "name": "Organization Pvt Ltd",
                    "logo": {
                        "url": "{{app-root-url}}/drive/files/605c47ee3c67843e85466.png"
                    },
                    "address": {
                        "line1": "4178, My Street",
                        "city": "SAS Nagar",
                        "state": "Punjab",
                        "pinCode": "161061",
                        "country": "India"
                   }
                },
                "status": "active",
                "timeStamp": "2021-03-25T08:21:02.104Z"
            }
        },
        "expiry": "2021-03-25T08:21:02.104Z",
        "status": "active"
   }
}
```

The session token would be used to authenticate the user on each request 

### Errors

Code    | Message
--------|----------
DILOPNT | Password not set
DILOINV | Invalid password or user-id



## Using OTP

TODO

## Using QR Code

TODO

## Using Google Auth

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

## Getting session using a token

The session can be obtained from the **directory** by sending the following request

* **Url**: `{{api-root-url}}/directory/api/sessions/current`
* **Type**: GET
* **Header**:

```yml
x-access-token: 1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY
```

The response would be the same as from the login request

### Errors

Code    | Message
--------|----------
DISGEXP | Session has expired
DISGINV | Invalid token

