
# Manage My Profile

## Get Profile

GET `{{api-root-url}}/directory/api/users/my`

## Upload Profile Image to Drive

upload the image file to

POST `{{api-root-url}}/drive/api/files?code=profile-image&folder-code=profile`

Response

```json
{
    "url" : "{{api-root-url}}/drive/images/636363663.png",
    "thumbnail": "data:image/png;base64,R0lGODlhyAAiALM...DfD0QAADs="
}
```

## Update Profile

PUT `{{api-root-url}}/directory/api/users/my`

```json
{
    "profile": {
        "firstName": "Sharukh",
        "lastName": "Khan",
        "gender": "male",
        "dob": "1976-10-10",
        "pic": {
            "url" : "{{api-root-url}}/drive/images/636363663.png",
            "thumbnail": "data:image/png;base64,R0lGODlhyAAiALM...DfD0QAADs="
        }
    }
}
```
