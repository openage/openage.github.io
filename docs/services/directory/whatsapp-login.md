# Whatsapp Login
Login with whatsapp validated Number

## Using Session

### Step 1: 

Send following request to
**Url**: `{{api-root-url}}/https://qa.yatrafreight.com/directory/api/users/auth/whatsapp/success`
**Type**: POST
**params**:

```JSON
{
"code": "confidential string",
"phone": "Phone no.",
"device": "Device name",
"app" : "Whatsapp"
}
```

The directory will
* Validate the confidential string
* Create a active session

**Response:**
```json
{
    "isSuccess": true,
    "data": { 
        "id": "63b81cdd6a513a001e712aec",
        "status": "active",
        "token": "cxcxcxcxcxcxcxc",
        "expiry": "2023-01-13T13:06:37.225Z",
        "user": {
            "id": "63ad392969a9ce001ff36c67",
            "email": "email@email.com",
            "phone": "phone",
            "status": "active",
            "profile": { },
            "identities": {},
            "isEmailValidate": false,
            "isProfileComplete": false,
            "isTemporary": false,
            "address": {},
            "roles": []
        }
    }
}
```

#### Errors

Code                   | Message
--------               |----------
TOKEN_INVALID          | Confidential string invalid
TOKEN_IS_REQUIRED      | Token is required
MOBILE_NUMBER_REQUIRED | Mobile number Required
USER_DOES_NOT_EXIST    | User does not exist
