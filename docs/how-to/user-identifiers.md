## What are the unique identifiers of the user

Following identifiers are unique across the sub-systems

- Email
- Mobile
- User Code
- User Id
- Employee Code (with organization code)
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