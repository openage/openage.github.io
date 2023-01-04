# Password Auth
#authentication #custom #plugin

Password auth can be used along with variours user [identifiers](/how-to/user-identifiers.md) .  Here are the identifiers you can use:
1. User Id,
2. Role Id,
4. Email 
5. Mobile
6. Employee Code (along with organization code)


Here is a sample request with email.  `POST` following body to the url: `{{api-root-url}}/directory/api/sessions`

```JSON
{
   "purpose": "login",
   "app": "chrome",
   "user": {
       "email": "example@organization.com",
       "password": "123123"
   }
}
```

The response will be the session object.

### Errors

| Code      | Message                     |
| --------- | --------------------------- |
| DI_LO_PNT | Password not set            |
| DI_LO_INV | Invalid password or user-id |

