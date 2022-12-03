# Passing credentials with a request

There are 2 types of credentials

Once you obtain the role-key from login you can pass it in one of the following ways

- in the header of every request

```json
{
    "x-role-key": "899eddde-2c5a-16df-7226-4c4116f3e351"
}
```

- in the query of every request

HTTPACTION `{{api-root-url}}/sendIt/api/messages?role-key=899eddde-2c5a-16df-7226-4c4116f3e351`

For a guest user, the tenant code must be passed. It can also be passed in header or query

```json
{
    "x-tenant-code": "inf"
}
```

- in the query of every request

HTTP ACTION `{{api-root-url}}/drive/api/files?tenant-code=inf`

The system identifies users based on the following logic

1. If the role key is passed. The sub-system goes to the auth service (the directory) and gets the details of the user (including its organization and tenant)
2. If only tenant code is passed the user is treated as a guest of the tenant


[[simple-report]]


