# Getting claims from token

#session #authentication 

There are 2 ways to get the claims from the session

## Getting session from API

The session can be obtained from the **directory** by  sending `GET` request to  `{{api-root-url}}/directory/api/sessions/current` with follwing header

```yml
x-access-token: 1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY
```

The response would be the same as from the login request.


## Parsing the JWT token

#todo