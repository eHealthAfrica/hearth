# JWT Authentication

## Generate a token

A token can be generated by POSTing a user's email address and password to the `/api/session` endpoint:

```bash
curl -XPOST -H 'Content-Type:application/json' -d '{"email": "sysadmin@jembi.org", "password": "sysadmin"}' localhost:3447/api/session
```

If the credentials are correct the response will be a JSON object containing a token:

```json
{
  "token": "eyJhb...zJbS0"
}
```

The debugger at https://jwt.io can be used to decode the token and view its contents.

## Authenticate a request

Once a token has been generated it should be included in the HTTP 'Authorization' header when making requests to private endpoints:

```
curl -XGET -H "Authorization: Bearer eyJhb...zJbS0" localhost:3447/fhir/Patient/1 
```

The token will then be verified and decoded to authenticate the user.
