# Login

#authentication #directory #login #session

Login request is a  session creation request. When `POST` following object to `{{api-root-url}}/directory/api/sessions`, a session is created and the users details are sent back

```JSON
{
   "purpose": "login",
   "app": "chrome",
   "user": {
       // credentials goes here
   }
}
```

A session request composes of, along with the credentials,  some meta information like
1. Purpose
2. Application

These fields works as  tags of the session. These tags helps-
- the users identify their active sessions. 
- the system customize the user's experience

Here is the sample `session` object returned by the system:

```JSON
{
	"id": "605c47eec0b3c67843e85466",
	"token": "1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY",
	"purpose": "login",
    "app": "chrome",
    "expiry": "2021-03-25T08:21:02.104Z",
	"user": {
		"email": "user@organization.com",
		"profile": {
		},
		"role": {
			"id": "605c47eec0b3c67843e85467",
			"key": "57605ffa-0ec4-a911-70c7-1edba4b70272",
			"code": "xxxxxxx",
			"permissions": ["organization.admin"],
			"type": {
				"id": "5fd4c92cb9ba1d02b98f8e2d",
				"code": "organization.admin",
				"name": "Organization Admin"
			},
			"employee": {},
			"organization": {},
			"status": "active"
		}
	},
	"status": "active"
}
```

## Login Plugins

The login behaviour can be modified using differnet plugins. For details checkout follwoing  plugins

1. [Password Login](/services/directory/auth-plugins/directory-password-auth.md)
2. [Custom Password Provider](/services/directory/auth-plugins/custom-password-auth.md)
3. [Active Directory Auth](/services/directory/auth-plugins/ad-auth.md)
4. [Google OAuth](/services/directory/auth-plugins/google-auth.md)
5. [QR Code Auth](/services/directory/auth-plugins/qr-code-auth.md)
6. [OTP Auth](/services/directory/auth-plugins/otp-auth.md)

