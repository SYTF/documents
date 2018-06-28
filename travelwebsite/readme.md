# API Document

## API endpoint
`http://dev.travelwebsite.com/api/`

## Authorization
`POST /auth/login`
### Request
```json
{
    "username" : "user",
    "password" : "pswd"
}
```
### Return Sample
```json
{
     "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7Il9pZCI6IjVhNWY4NmIxOTdmYjU4N2NjYzJhMzhiZiIsInVzZXJuYW1lIjoic3V..."
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
`POST /serviceTyps`
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
