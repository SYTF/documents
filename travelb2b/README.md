# API Document

## API endpoint
`https://dev.travelbearb2b.com/api/`

--- 

## Request Sample
Making request to our API endpoint is super easy. Please prepare an access token and embed it to the request header. Excluding receiving access token and refresh token endpoint. 

```
curl -X POST -H “Authorization: Bearer <ACCESS_TOKEN>" https://dev.travelbearb2b.com/api/auth/check
```
--- 

## Authentication
### Receiving an access token
Most of the APIs are required an access token for authenticating. You can use `username` and `password` to request a user based access token. 
> POST /auth/login

#### Body
```json
{
	"username" : "user1",
	"password" : "user1 password"
}
```
#### Return
```json
{
	"token" : "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V…"
}
```

### Token Validation
Used to check the token validated or not. This API will return the user information.
>`POST /auth/check`

#### Return
```json
{
    "username": "agentA",
    "email": "test@agent.com",
    "type": "agent_superuser",
    "name": "Agent A",
    "timezone": "UTC",
    "currency": "HKD"
}
```
