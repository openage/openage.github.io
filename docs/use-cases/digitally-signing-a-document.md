
## Getting signature on a file

## Making the system ready for signature

Setup the signature provider

PUT `{{api-root-url}}/drive/api/tenants/my`

```json
{
    "sign": {
        "provider": "genie-sign",
        "config": {
            "url": "https://www.esigngenie.com/esign/api",
            "apikey": "418.....ff1",
            "clientSecret": "e363ac8....72476"
        }
    }
}
```

Note you need to configure the signing provider to the callback

POST `{{api-root-url}}/drive/api/files/genie-sign/callback`

## Sending the file for signature

Step 1: Upload the file (need to be a doc file) to `{{api-root-url}}/drive/api/files` with params in the query string, something like following

```
folder-code: root|contracts
entity-id: 1
entity-type: contract
status: draft
code: contract-1
name: Contract 1
```

Step 2: Submit the file for signature

PUT following in `{{api-root-url}}/drive/api/files/contract-1?entity-id=1&entity-type=contract`

It has 3 attributes

1. add the `signers` to the file
2. tell the drive API what to do (`hooks`) when the file is set to `active`
3. tell the drive API that you are `submitting` the file for signature

```json
{
    "signers": [{
        "email": "sunny.parkash@gmail.com",
        "profile": {
            "firstName": "Sunny",
            "lastName": "Parkash"
        },
        "meta": {
            "organization": "Hospital 1",
            "title": "Director"
        }
    }],
    "hooks": [{
        "trigger": "active",
        "url": "http://api.servana.com/core/api/contracts/1",
        "action": "POST",
        "config": {
            "headers": {
                "x-role-key": "xxx-yyyy-zzzz"
            }
        },
        "data": {
            "status": "active"
        }
    }],
    "status": "submitted"
}
```

## Instructions for testing

Activate the file by setting its status via update api.

PUT to `{{api-root-url}}/drive/api/files/contract-1?entity-id=1&entity-type=contract` with following payload

```json
{
    "status": "active"
}
```

Note:

- It is recommended you follow `draft`-`submitted`-`active` workflow for a file
- The system will also keep track the status `signed`-`viewed`-`signed` of signatures. You can get it via GET `{{api-root-url}}/drive/api/files/contract-1?entity-id=1&entity-type=contract`
