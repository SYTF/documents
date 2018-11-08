# API Document

## Table of Content
- [API Endpoint](#api-endpoint)
- [Request Sample](#request-sample)
- [Authenication](#authentication)
	- [Receiving an access token](#receiving-an-access-token)
	- [Token Validation](#token-validation)
- [Package](#package)
	- [Package List](#package-list)

## API endpoint
`https://www.travelbearb2b.com/api/`

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

## Package
### Package List
> POST /agent/package

#### Body
| Param | Default | Description |
| ------------- | ------------- |
|startDate|Start day of current month|Optional. Date for filtering the packages|
|endDate|End day of current month|Optional. Date for filtering the packages|
|country|empty|Optional. Filter packages by country code. Please ref. to the country list API.|
|type|empty|Optional. Filter packages by service type. Please ref. to the service type API.|
|page|1|Optional. For switching pages|
|perPage|10|Optional. Control the number of returning items|

#### Return
```json
{
    "totalItems": 7,
    "totalPage": 1,
    "currentPage": 1,
    "data": [
        {
            "_id": "5b334510770d8976f8d82ce5",
            "themeCode": "JP-NRT-TUR-17022",
            "country": "JP",
            "city": "NRT",
            "type": "TUR",
            "name": {
                "en": "[Licensed Green Label Vehicle & Departure From 2] Mt Fuji + Onsen One Day Tour (Tokyo Hotel Pickup)",
                "zh": "【綠牌車2人成團】富士山、忍野八海、溫泉  一天遊  (東京市區酒店專車接送) "
            },
            "description": {
                "en": "",
                "zh": ""
            },
            "remark": {
                "en": "",
                "zh": ""
            },
            "plans": [
                {
                    "code": "A",
                    "name": {
                        "en": "Mt. Fuji & Onsei One day tour - per person",
                        "zh": "富士山、溫泉一天遊 - 每位"
                    }
                }, {…}
            ],
            "created_at": "2018-06-27T08:04:32Z",
            "updated_at": "2018-06-27T08:04:32Z",
            "status": "AP",
            "dateRange": {
                "startDate": "2018-07-02",
                "endDate": "2018-08-31"
            }
        }, {…}
    ]
}
```

### Specific Product [WIP]
> POST /agent/product/:packageID

#### Return
```json
	"package" : {
		"themeCode": "TH-HHQ-TUR-111",
		"details": [],
	},
	"questionnaire" : {
	}
```
