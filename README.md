# Visibility Documentation
## Authentication

`POST /authenticate`

#### Fields Body

| field    | description      | required | example |
| -------- | ---------------- | -------- | ------- |
| email    | email of user    | Yes      | 1       |
| password | password of user | Yes      | 123456   |

#### Request Body
```
{
    "email": "luca123@gmail.com",
    "password": "123456"
}
```

#### Response Body

```
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJadwq6MSwiZW1haWwiOiJhbGFuc2FudGFuYUBhbHVub3MudXRmcHIuZWR1LmJyIiwicGhvbmVfbnVtYmVyIjoiOTk4MDgtMzAxNyIsImlhdCI6MTYzMzcyOTk5MiwiZXhwIjoxNjMzOTAyNzkyfQ.pYTLcIAEnwONb9R53pJplQL2s_fthALWPIcq4aMUf2Q"
}
```
#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |

## Markers
### Post Marker
`POST /markers`

#### Fields Body

| field           | description           | required | types                                                                                        | example                         |
| --------------- | --------------------- | -------- | -------------------------------------------------------------------------------------------- | ------------------------------- |
| user_id         | id of user            | Yes      |                                                                                              | 1                               |
| markers_type_id | id of type of marker  | Yes      | PLACE, WHEELCHAIR_PARKING                                                                    | PLACE                           |
| coordinates     | coordinates of marker | Yes      |                                                                                              | POINT (-50.3826153 -28.0245769) |
| category_id     | id of category        | No       | TRAVEL,TRANSPORT,SUPERMARKET,SERVICES,LEISURE,EDUCATION,FOOD,HOSPITALS,ACCOMMODATION,FINANCE | SERVICES                        |
| name            | name of place         | No       |                                                                                              | Mac Burguer                     |
| classify        | classify of place     | No       | ACCESSIBLE, NOT ACCESSIBLE, PARTIALLY                                                        | ACESSIBLE                       |
| description     | description of place  | No       |                                                                                              | Lanchonete e petiscaria         |
| space_type      | type of space         | No       | PRIVATE,PUBLIC                                                                               | PRIVATE                         |


#### Request Body

```
{
    "user_id": 5,
    "marker": {
        "markers_type_id": "PLACE",
        "category_id": "EDUCATION"
    },
    "point_data": {
        "latitude": -28.0245769,
        "longitude": -50.3826153
    },
    "place": {
        "name": "Mac Burguer",
        "classify": "ACCESSIBLE",
        "description": "Lanchonete e petiscaria",
        "space_type": "PRIVATE" 
    }
}
```

#### Response Body

```
{
    "id": 56,
    "user_id": 1,
    "markers_type_id": "PLACE",
    "coordinates": "POINT(-50.3826153 -28.0245769)"
}

```

#### Responses Code

| code | description |
| ---- | ----------- |
| 201  | created     |


### Get Markers with current position

`GET /markers/:current_position`

#### Request Params

| field            | description              | example                         |
| ---------------- | ------------------------ | ------------------------------- |
| current_position | current position of user | POINT (-50.3826153 -28.0245769) |


#### Response Body

```
[
    {
        "id": 30,
        "user_id": 1,
        "markers_type_id": "PLACE",
        "coordinates": "POINT(-51.382978 -26.024556)",
        "last_updated": null,
        "denounced": false,
        "category_id": "EDUCATION"
    }
]

```
#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |


### Get Markers with id
`GET /markers/places/:marker_id`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| marker_id | id of marker | 1       |


#### Response Body

```
{
    "id": 44,
    "marker_id": 42,
    "name": "Mac Burguer",
    "classify": "PARTIALLY",
    "space_type": "PRIVATE",
    "description": "Lanchonete e petiscaria"
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |

## Gamification
### Get Ranking
`GET /ranking`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| page      | page of users| 1       |

#### Response Body

```
{

    "pagination": {
        "total": 15,
        "lastPage": 2,
        "perPage": 10,
        "currentPage": 1,
        "from": 0,
        "to": 10
    },

    "data": [
        {
            "name": "Rodrigo Santos",
            "weekly_points": 1000,
            "level": 1
        },
        {
            "name": "kawamoto",
            "weekly_points": 800,
            "level": 2
        }
    ]
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |


### Patch Information Amount
`PATCH /users/:id/informationAmount`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of users  | 1       |

#### Response Body

```
{
    "updatedProperties": ["wheelchair_parking"],
    "points": 10
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |
### Get Information Amount
`GET /users/:id/informationAmount`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of users  | 1       |

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |
### Get achievements
`GET /users/:id/achievements`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of users  | 1       |

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |
### Get comments
`GET /markers/:id/comments`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of comment| 1       |

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |
### Post comment
`POST /markers/:id/comments`

```
{
    "userId": 1,
    "markerId": 1,
    "description": "Parabéns!"
}
```

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of comment| 1       |

#### Responses Code

| code | description |
| ---- | ----------- |
| 201  | created          |

## Users
### Patch user
`PATCH /users/:id(\\d+)`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of user   | 1       |

#### Response Body

```
{
    "name": "carlos@gmail.com",
    "phone_number": "44998433695",
    "birth_date": "1998-01-01"
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |
### Post user
`PATCH /users`

#### Request Body
```
{
    "name": "lucas silvano",
    "birthDate": "1998-01-01",
    "gender": "MALE",
    "phoneNumber": "4499887565",
    "email": "lucas321@gmail.com",
    "password": "123456"
}
```

#### Response Body

```
{
	"id": 2
    "birth_date": "1998-01-01",
    "gender": "MALE",
	"phone_number": "4499887565",
	"email": "lucas321@gmail.com",
	"password": "123456"
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 201  | created          |
### Get user
`GET /users/:id`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| id        | id of user   | 1       |

#### Response Body

```
{
    "id": 1,
    "name": "ADMIN",
    "phone_number": "99702-3015",
    "birth_date": "1992-12-21T02:00:00.000Z"
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |

### Update password
`PATCH /users/passwords/:user_id`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| user_id   | id of user   | 1       |

#### Response Body

```
{
    "current_password": "masterkey",
    "new_password": "123456"
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | OK          |
### Recovery password
`PATCH /users/:email`

- Send email with new password 

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| email     | email of user| 1       |

#### Response Body

```
{}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 204  | OK          |
