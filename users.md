# Users
You can use this API for managing various behaviour of users

## Login or Register & Update Profile

You can use this endpoint to create new user if it does not exist yet, or you can use this endpoint to update data of the user if they already exists. You can send a extra data in user's data by using **extras** payload , such as you want to add user type, then you can put key as user_type and put your desired value.

verb :
`POST /api/v2.1/rest/login_or_register`

request :

```bash
user_id [string]
password [string password, optional] # if password is provided and user exists, the user's password will be updated
username [string]
avatar_url [string url, optional]
extras [JSONstring, optional] or valid JSON object
```

Note : `password` is optional, it will generate random string on the backend if you dont pass it during `User` creation through this API. However, please note for those users already created you can not use this API `login_or_register` without passing password value

response :

```json
{
    "results": {
        "user": {
            "user_id": "user@email.com",
            "username": "Johnny Cage",
            "avatar_url": "https://myimagebucket.com/image.jpg",
            "extras": {
                    "key": "value",
                    "key1": "value1"
            }
        },
    },
    "status": 200
}
```

## Get User Profile
You can get user profile by using this API

verb:
`GET /api/v2.1/rest/user_profile`

request:
```bash
user_id [string] required
```

response:
```json
{
    "results": {
        "user": {
            "user_id": "user@email.com",
            "username": "Johnny Cage",
            "avatar_url": "https://myimagebucket.com/image.jpg"
        },
    },
    "status": 200
}
```

## Get Unread Users
This intended to get user_id that have unread messages

verb: `GET /api/v2.1/rest/get_unread_users`

request:
```bash
page 
limit - default is 100 , the value is beetween 1-100, otherwise will override to 100
start_time  [string] in format "YYYY-MM-DD hh:mm:ss"
end_time    [string] in format "YYYY-MM-DD hh:mm:ss"
``` 

response:
```json
{
    "results": {
        "user_ids": [
            "userid_1",
            "userid_2"
        ]
    },
    "status": 200
}
```


## Get User Unread Count
This intended to get user_id that have unread messages

verb: `GET /api/v2.1/rest/get_user_unread_count`

request:
```bash
user_ids    [array of string] *required*
start_time  [string] in format "YYYY-MM-DD hh:mm:ss"
end_time    [string] in format "YYYY-MM-DD hh:mm:ss"
```

response :

```
 {
     "results": {
        "user_unread_count": [
             {
                 "unread_count": 14,
                 "user_id": "user1@qiscus.com"
             },
             {
                 "unread_count": 71,
                 "user_id": "user2@qiscus.com"
             }
         ]
     },
     "status": 200
 }
 ```

## Get All Users
You can get all registered users by calling this API

verb:
`GET /api/v2.1/rest/get_user_list`

request:
```bash
page [int]
limit [int]
order_query [string] example: created_at desc nulls last
```

response:
```json

{
    "results": {
        "meta": {
            "total_data": 3147,
            "total_page": 1573
        },
        "users": [
            {
                "avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
                "created_at": "2017-10-09T06:47:00.004482Z",
                "email": "\"\"",
                "id": 185284,
                "name": "A. Athaullah",
                "updated_at": "2017-10-09T06:47:00.004482Z",
                "username": "A. Athaullah"
            },
            {
                "avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
                "created_at": "2017-09-18T04:15:04Z",
                "email": "081111111111@qiscuswa.com",
                "id": 178,
                "name": "iPhone test User",
                "updated_at": "2017-09-18T04:15:04Z",
                "username": "iPhone test User"
            }
        ]
    },
    "status": 200
}
```
