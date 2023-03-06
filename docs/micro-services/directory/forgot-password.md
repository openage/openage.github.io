# Forgot Password
The signup is 2 step process

## Using Session

### Step 1: Send OTP By Email

Send following request to
**Url**: `{{api-root-url}}/directory/api/users/resend`
**Type**: POST
**Body**:

```JSON
{
    "app": "web",
    "device": "Chrome",
    "purpose": "forgot-password",
    "email": "email@email.com",
    "templateCode": "directory|session-forgot", // Template config to send in email
}
```

The directory will
* Create a new session 
* Generate a OTP in session and user
* Send notification to SEND-It to send Email

**Response:**
```json
{
    "isSuccess": true,
    "data": {
        "id": "{{user_id}}", // User id
        "session": {
            "id": "{{session_id}}",
            "timeStamp": "2023-01-06T06:25:41.227Z",
            "status": "awaiting"
        }
    }
}
```

## Two Ways to do this 

### Step 2.1.1: Validate the OTP first

To validate the session 
* OTP 
* Session
* User

Send following request to
**Url**: `{{api-root-url}}/directory/api/users/setPassword`
**Type**: POST
**Body**:

```JSON
{
    "id": "{{user_id}}", // User Id
    "session": "{{session_id}}", // Session Id
    "otp": "112233"
}
```

The directory will
* Validate the otp
* Clear the otp 
* Mark the session validated


**Response:**
```json
{
    "isSuccess": true,
    "data": { // User Object
        "id": "60115a65c0c6974f894f9ea6",
        "email": "email@email.com",
        "phone": "phone",
        "status": "active",
        "profile": {},
        "meta": {},
        "identities": {},
        "isEmailValidate": true,
        "isProfileComplete": false,
        "isTemporary": false,
        "address": {},
        "roles": []
    }
}
```

### Step 2.1.2: Set Password

To validate the session 
* Password 
* Session
* User

Send following request to
**Url**: `{{api-root-url}}/directory/api/users/setPassword`
**Type**: POST
**Body**:

```JSON
{
    "id": "{{user_id}}", // User Id
    "session": "{{session_id}}", // Session Id
    "password": ""
}
```

The directory will
* Validate session is it validated
* Set the Password


**Response:**
```json
{
    "isSuccess": true,
    "data": { // User Object
        "id": "60115a65c0c6974f894f9ea6",
        "email": "email@email.com",
        "phone": "phone",
        "status": "active",
        "profile": {},
        "meta": {},
        "identities": {},
        "isEmailValidate": true,
        "isProfileComplete": false,
        "isTemporary": false,
        "address": {},
        "roles": []
    }
}
```

### Step 2.2.1: Validate OTP and Set the password in one request

To validate the session and set the password
* OTP 
* Session
* User
* Password

Send following request to
**Url**: `{{api-root-url}}/directory/api/users/setPassword`
**Type**: POST
**Body**:

```JSON
{
    "id": "{{user_id}}", // User Id
    "session": "{{session_id}}", // Session Id
    "otp": "112233",
    "password": ""
}
```

The directory will
* Validate the otp
* Clear the otp 
* Mark the session active
* set the password


**Response:**
```json
{
    "isSuccess": true,
    "data": { // User Object
        "id": "60115a65c0c6974f894f9ea6",
        "email": "email@email.com",
        "phone": "phone",
        "status": "active",
        "profile": {},
        "meta": {},
        "identities": {},
        "isEmailValidate": true,
        "isProfileComplete": false,
        "isTemporary": false,
        "address": {},
        "roles": []
    }
}
```

#### Errors

Code        | Message
--------    |----------
DI_USP_PRQ  | Password Required
DI_UVO_UDNE | User Does not exists
DI_UVO_OINV | Otp is invalid
DI_UVO_UBKD | User is blocked
DI_USC_SDNE | Session does not exists
DI_USC_SE   | Session Expired
DI_USC_SAE  | Session Attempts excited
