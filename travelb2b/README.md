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
    "_id": "5ae56e585102193d8cbe0b81",
    "username": "TestAgent",
    "email": "test@agent.com",
    "type": "agent_superuser",
    "name": "TestAgent",
    "timezone": "UTC",
    "currency": "HKD"
}
```


## Country List
`POST /location`
### Header
```json
{
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V..."
}
```
### Request
no need to pass anythings
### Return Sample
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
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V..."
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

## Get Products
`POST /agent/package`
### Header
```json
{
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V..."
}
```
### Request
|Param|Default|Description|
| ------------- | ------------- | ------------- |
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
                }, {...}
            ],
            "created_at": "2018-06-27T08:04:32Z",
            "updated_at": "2018-06-27T08:04:32Z",
            "status": "AP",
            "dateRange": {
                "startDate": "2018-07-02",
                "endDate": "2018-08-31"
            }
        }, {...}
    ]
}
```

## Get Specific Product
`POST /agent/package/:packageID`
### Header
```json
{
    "Authorization" : "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V..."
}
```
