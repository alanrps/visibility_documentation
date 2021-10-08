# Documentation

## Authentication

`POST /authenticate`

#### Fields Body

| field    | description      | required | example |
| -------- | ---------------- | -------- | ------- |
| email    | email of user    | Yes      | 1       |
| password | password of user | Yes      | PLACE   |

#### Request Body
```
{
    "email": "matheus@gmail.com",
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
| 201  | created     |

## Markers

### Create Markers


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
| 200  | ok          |


### Get Markers with id
`GET /markers/places/:marker_id`

#### Request Params

| field     | description  | example |
| --------- | ------------ | ------- |
| marker_id | id of marker | 1       |


### Response Body

```
{
    "id": 44,
    "marker_id": 42,
    "name": "terreno",
    "classify": "PARTIALLY",
    "space_type": "PRIVATE",
    "description": "belo terreno"
}
```

#### Responses Code

| code | description |
| ---- | ----------- |
| 200  | ok          |
