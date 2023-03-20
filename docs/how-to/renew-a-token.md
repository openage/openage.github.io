# Renew A ToKEn

A token has a set expiry  time from the time of issue. So the token , after set period, will expire even while the user may be taking the action. This would break the user experience.

There are 2 approach to this

1. Take the user to login page
2. Renew the token when the user is still interacting with the system.

## Renew the token

When the user logs in 

`{{api-root-url}}/directory/api/users/signIn`

The api returns the session object along with the `current token` and` refresh token`

```JSON
{
	"isSuccess": true,
	"data": {
		"id": "6418782b80fa6a6b1679f608",
		"status": "active",
		"token": "xxxxxxx.....xxxxxx",
		"expiry": "2023-03-21T15:13:47.407Z",
		"refresh": {
			"token": "yyyyyy.....yyyyy",
			"expiry": "2023-03-21T15:18:47.409Z"
		},
		"user": {
		},
		"role": {
		}
	}
}
```

The expiration of the `refresh token`  is offset by few minutes.

When the user tries to used the `expired token` , the server would return  unauthorised  error. The application can use this event to trigger the renew the toke n by using the `refresh- token`

This can be done by `POST`ing  following body to renew api

API: `{{api-root-url}}/directory/sessions/{{session-id}}/renew`
Body:
```JSON
{
	"refresh": {
		"token": "yyyyyy.....yyyyy"
	}
}
```

The api would respond with the valid token along with the new refresh token
```JSON
{
	"isSuccess": true,
	"data": {
		"id": "6418782b80fa6a6b1679f608",
		"token": "aaaaaa......aaaaaaa",
		"expiry": "2023-03-21T10:18:55.771Z",
		"refresh": {
			"token": "bbbbbbb......bbbbbb",
			"expiry": "2023-03-21T10:23:58.328Z"
		}
	}
}
```

### Redirection to Login

When the application tries to renew the token, it is possibility that the user has been idle for long enough, and the  `refresh token` has also expired. In that case, there is no option but to logout the user and take him to login page.

The application needs would be redirected to 

`https://id.domain.com/login?redirect=https://app.domain.com/settings`

### Configuring the Token

Token configuration can be managed in the directory tenant

```JSON
{
	"config" : {
        "auth" : {
            "provider" : "directory",
            "autoCreate" : true
        },
        "auths" : {
            "directory" : {
                "secret" : "qwqwqw..qwewe",
                "period" : 1440,
                "refresh" : {
                    "secret" : "qwqwqw..qwewe",
                    "period" : 1445
                }
            }
        }
    }
}
```

Note: the `refresh.period`  is 5 minutes more than the token `period`
