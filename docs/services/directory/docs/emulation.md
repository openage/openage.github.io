# Emulation

The directory allows a user (with the right permissions) to emulate another organization's role or user. For this it uses sessions

## Emulating a Role in other organization

To impersonate a role, create an impersonate session specifying the `role type` and the `organization`

Send the following request to

* **Url**: `{{api-root-url}}/directory/api/sessions`
* **Type**: POST
* **Header**
```yml
x-access-token: 1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY
```
* **Body**:

```JSON
{
    "purpose": "impersonate",
    "app": "chrome",
    "meta": {
        "organization": {
            "code": "organization"
        },
        "role": {
            "type": {
                "code": "organization.admin"
            }
        }
   }
}
```

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
                "permissions": ["organization.admin"],
                "type": {
                    "id": "5fd4c92cb9ba1d02b98f8e2d",
                    "code": "organization.admin",
                    "name": "Organization Admin",
                    "status": "active",
                    "timeStamp": "2021-05-31T04:52:39.317Z"
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

## Impersonating a user

TODO