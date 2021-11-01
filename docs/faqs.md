# FAQ

## How do I pass credentials with a request

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

## What are the unique identifiers of the user

Following identifiers are unique across the sub-systems

- Email
- Mobile
- Code
- Role Id
- Role Code

## What is a role

The role is a set of attributes and credentials that uniquely identifies the user and determines what the user can/cannot do within the system. Following are the attributes of a role

- id: the unique id which is in the public domain
- key: the secret using which the requesting user is identified by the server
- code: a user-friendly code. `my` and `system` are reserved for the current user and system owner respectively
- permissions: a set of strings normally in format `{area}.{scope}`. 
  - An organization-specific role would have `organization.user` + `organization.*`. 
  - A tenant-level role would have `tenant.user` + `tenant.*`
  - A guest user would have `tenant.guest`
- profile: each role can have a different profile and avatar. This incudes name, pic, email etc
- organization: in case the role belongs to an organization

A user can have multiple roles within the system, some of them would grant the user the rights within an organization, some of them would be system-level roles

## Why I cannot upload my pic before I complete the signup

The system(dive) needs a role-key to receive any file. And the key is only available to the logged-in user.

This is done to prevent anyone from running DOS attack and fill the space of the server.