# API Document

## Table of Content
- [API Endpoint](#api-endpoint)
- [Request Sample](#request-sample)
- [Authenication](#authentication)
	- [Receiving an access token](#receiving-an-access-token)
	- [Token Validation](#token-validation)
- [Package List](#package-list)
- [Order](#submit-order)

## API Endpoint
`https://www.travelbearb2b.com/api/`

— 

## Request Sample
Making request to our API endpoint is super easy. Please prepare an access token and embed it to the request header. Excluding receiving access token and refresh token endpoint. 

```
curl -X POST -H “Authorization: Bearer <ACCESS_TOKEN>" https://dev.travelbearb2b.com/api/auth/check
```
— 

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

### Refresh
Every access token will be expired in 2 hours. You may request a new one before the token expire. 
> POST /auth/token/refresh

#### Return
```json
{
	"token" : "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V…"
}
```

### Token Validation
Used to check token validated or not. This API will return the user information.
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

—

## Packages
All package related APIs are included. Such as available countries, regions, package types for searching and packages. 
### Country List
> POST /location/countries

#### Request
```json
{
    perPage : 10,
    page : 1```
#### Return
```json
{
    "totalItems": 1,
    "totalPage": 1,
    "currentPage": 1,
    "data": [
        {
            "_id": "5aa155bd602a9c0c1a24cc67",
            "name": {
                "en": "Hong Kong",
                "zh": "香港"
            },
            "latlng": [
                22.25,
                114.16666666
            ],
            "code": "HK",
            "callingCode": "852",
            "region": "Asia",
            "currency": {
                "code": "HKD",
                "name": "Hong Kong dollar",
                "symbol": "$"
            },
            "timezone": "UTC+08:00",
            "cities": [
                {
                    "code": "NT",
                    "name": {
                        "en": "New Territories",
                        "zh": " 新界"
                    }
                },
                {
                    "code": "KL",
                    "name": {
                        "en": "Kowloon",
                        "zh": "九龍半島"
                    }
                }
            ]
        }
    ]
}
```

## Service Type
`POST /serviceTypes`
### Header
```json
{
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V…"
}
```
### Request
no need to pass anythings
### Return Sample
```json
[
    {
        "type" : "TUR",
        "name" : {
            "en" : "Tour",
            "zh" : "旅行"
        }
    },
    {
        "type" : "TIC",
        "name" : {
            "en" : "Ticket",
            "zh" : "門票"
        }
    }
]
```

## Package List
`POST /agent/package`

### Request
|Param|Default|Description|
| —————— | —————— | —————— |
|startDate|Start day of current month|Optional. Date for filtering the packages|
|endDate|End day of current month|Optional. Date for filtering the packages|
|country|empty|Optional. Filter packages by country code. Please ref. to the country list API.|
|type|empty|Optional. Filter packages by service type. Please ref. to the service type API.|
|page|1|Optional. For switching pages|
|perPage|10|Optional. Control the number of returning items|
### Return Sample
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

## Get Specific Product
`POST /agent/package/:packageID`
### Header
```json
{
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V…"
}
```

## Submit Order
`POST /order/submit`
### Header
```json
{
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V…"
}
```
### Request
|Param|Default|Description|
| —————— | —————— | —————— |
|packageID|String :: Please ref. to the package field (_id).|
|date|String :: The date of departure with date format YYYY-MM-DD|
|visitors|[]|Object Array :: Contains all the information about the traveler. Fields are listed below.|
|visitors.plan|empty|String :: The plan code which selected. ref. to package.plan|
|visitors.priceType|empty|String :: adult / child|
|visitors.questions|[]|Contains the repeat questions only. eg: questions.repeat == true|
|questions|[]|Object Array :: Contains all the fields of the non-repeat questions. eg: questions.repeat == false |
|questions.value|empty|String :: The value of each questions.|
|contactInfo|{}|Object :: An Object for storing contact information. Fields are listed below.|
|contactInfo.name|empty|String :: The name of contact person.|
|contactInfo.phoneNumber|empty|String :: The phone number of contact person.|
|contactInfo.email|empty|String :: The email address of contact person.|
