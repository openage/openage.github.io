# Signup
The signup is 2 step process

## Using Session

### Step 1: Initiate a new session

Send following request to
**Url**: `{{api-root-url}}/directory/api/sessions`
**Type**: POST
**Body**:

```JSON
{
   "purpose": "signup",
   "app": "www",
   "user": {
       "email": "admin@organization.com",
       "profile": {
           "firstName": "Organization",
           "lastName": "Admin"
       },
       "password": "123123"
   },
   "meta": {
       "organization": {
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
           },
           "meta": {
               "gst": ""
            }
        },
        "source": {
           "type": "referral",
           "code": "AGT123"
       }
   }
}
```

The directory will
* Create a new session 
* Create a user (if it does not already exist)
* Send out (email) a link to the user to activate the session 
* Send out a pending session to the user

**Response:**
```json
{
   "isSuccess": true,
   "message": "Please check your email to complete the signup",
   "data": {
       "id": "605c47eec0b3c67843e85466",
       "expiry": "2021-03-25T08:21:02.104Z",
       "status": "awaiting"
   }
}
```

### Step 2: Activate the Session

Session can be activated using one of the following secrets
* Token 
* OTP

The user would come to the application with following url
`{{app-root-url}}?session-id=605c47eec0b3c67843e85466&access-token=1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY`

This has two parameters in the query
* Session Id 
* Session Token

The application, when it renders the link, would send the link to the session api to activate and log in

* Url: `{{api-root-url}}/directory/api/sessions/605c47eec0b3c67843e85466`
* Type: PUT
* Body:

```json
{
    "token": "1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY",
    "status": "active"
}
```
Or
```json
{
    "otp": "000000",
    "status": "active"
}
```




The API would respond with
```json
{
   "isSuccess": true,
   "message": "Signup Complete. Please Login",
   "data": {
       "id": "605c47eec0b3c67843e85466",
       "token": "1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY",
       "expiry": "2021-03-25T08:21:02.104Z",
       "user": {
           "email": "admin@organization.com",
           "profile": {
               "firstName": "Organization",
               "lastName": "Admin",
               "pic": {
                   "url": "{{app-root-url}}/drive/files/605c67843e85466.png"
               }
           }
       },
       "status": "active"
   }
}
```

Post session activation directory will add a `offline.queue('session', session, 'active', context)`
* Will create a role based on the `session.meta`

#### Errors

Code    | Message
--------|----------
DISAEXP | Activation link has expired
DISAINV | Activation link is invalid


## Using Google Id

TODO

