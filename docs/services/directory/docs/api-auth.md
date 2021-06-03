# User authentication at API

## Authentication a user using the token

The token would be sent to the API either in the header  `x-access-token` or in the query `access-token`

The API's would fetch the session from the **directory** by sending the following request

* **Url**: `{{api-root-url}}/directory/api/sessions/my`
* **Type**: GET
* **Header**:

```yml
x-access-token: 1lIMjth4Gnv1KlbDtB7LsLY7xyoh3-rhJOcLhbxFARSY
```

### Errors

Code    | Message
--------|----------
DISGEXP | Session has expired
DISGINV | Invalid token