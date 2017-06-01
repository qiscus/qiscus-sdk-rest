# REST API

BASE_URL : [APP_ID].qiscus.com

example : if your APP_ID is `domino-prod` means the base_url will be `domino-prod.qiscus.com`

## Authentication

Add `secret key` on every header's request, you can get the value from dashboard.qiscus.com

## Create room

verb:

```
POST /api/v2/rest/create_room
```


request:

```
name [string]
participants[] [array of string email]
creator [string email]
```

response:

```
{
  "results": {
    "creator": "abc@outlook.com",
    "participants": [
      "abc@outlook.com",
      "kotak@outlook.com"
    ],
    "room_id": 16,
    "room_name": "gege",
    "room_type": "group"
  },
  "status": 200
}
```

## Get or create room with target

verb:

```
GET /api/v2/rest/get_or_create_room_with_target
```


request:

```
emails[] [array of string] # must contains 2 emails
avatar_url [string optional]
```

response:

```
{
  "results": {
    "comments": [
      {
        "comment_before_id": 124973,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124974,
        "message": "testingasdad asdas dasd",
        "timestamp": "2017-02-07T19:01:00Z",
        "unique_temp_id": "pyRIKY4reRXlU4Sp6r97",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      },
      {
        "comment_before_id": 124972,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124973,
        "message": "testingasdad asdas dasd",
        "timestamp": "2017-02-07T19:00:58Z",
        "unique_temp_id": "K5E6HmKQJQwSovEkFhHf",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      }
    ],
    "room": {
      "avatar_url": "",
      "chat_type": "single",
      "id": 234,
      "last_comment_id": 124974,
      "last_comment_message": "testingasdad asdas dasd",
      "last_topic_id": 234,
      "options": null,
      "participants": [
        {
          "avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
          "email": "abc@outlook.com",
          "username": "abc"
        },
        {
          "avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
          "email": "kotak@outlook.com",
          "username": "kotak"
        }
      ],
      "room_name": "abc@outlook.com kotak@outlook.com"
    }
  },
  "status": 200
}
```

## Get rooms info

verb:

```
POST /api/v2/rest/get_rooms_info
```


request:

```
room_id[] [array of string]
user_email [string email]
```

response:

```
{
  "results": {
    "rooms_info": [
      {
        "last_comment_id": 0,
        "last_comment_message": "",
        "last_comment_timestamp": "0001-01-01T00:00:00Z",
        "room_id": 13,
        "room_name": "abc@outlook.com kotak1@outlook.com",
        "room_type": "single",
        "unread_count": 123
      },
      {
        "last_comment_id": 0,
        "last_comment_message": "",
        "last_comment_timestamp": "0001-01-01T00:00:00Z",
        "room_id": 14,
        "room_name": "abc@outlook.com kotak2@outlook.com",
        "room_type": "single",
        "unread_count": 123
      }
    ]
  },
  "status": 200
}
```

## Add room participants

verb:

```
post /api/v2/rest/add_room_participants
```

request:

```
room_id [integer]
emails [array of string emails]
```

response:

```
{
  "results": {
    "creator": "abc@outlook.com",
    # updated participants
    "participants": [
      "abc@outlook.com",
      "kotak@outlook.com"
    ],
    "room_id": 16,
    "room_name": "gege",
    "room_type": "group"
  },
  "status": 200
}
```

## Remove room participants

verb:

```
post /api/v2/rest/remove_room_participants
```

request:

```
room_id [integer]
emails [array of string emails]
```

response:

```
{
  "results": {
    "creator": "abc@outlook.com",
    # updated participants
    "participants": [
      "abc@outlook.com",
      "kotak@outlook.com"
    ],
    "room_id": 16,
    "room_name": "gege",
    "room_type": "group"
  },
  "status": 200
}
```

## Post comment 

verb:

```
post /api/v2/rest/post_comment
```

request:

```
sender_email [string]
room_id [integer]
message [string]
```

response:

```
{
    "status": 200,
    "results": {
       "comment": {
            "id": 985,
            "comment_before_id": 984,
            "message": "Hello Post 2",
            "disable_link_preview": false,
            "email": "f1@gmail.com",
            "username": "f1",
            "user_avatar_url": "http://imagebucket.com/image.jpg",
            "timestamp": "2016-09-06T16:18:50+00:00",
            "unique_temp_id": "CanBeAnything1234321"
        }
     }
}
```

## Load comments

verb:

```
post /api/v2/rest/load_comments
```

request:

```
room_id [integer]
page [int optional]
limit [int optional default=20]
```

response:

```
{
  "results": {
    "comments": [
      {
        "comment_before_id": 124973,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124974,
        "message": "testing",
        "room_id": 234,
        "room_name": "abc@outlook.com kotak@outlook.com",
        "timestamp": "2017-02-07T19:01:00Z",
        "unique_temp_id": "pyRIKY4reRXlU4Sp6r97",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      },
      {
        "comment_before_id": 124972,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124973,
        "message": "here is the message that I sent",
        "room_id": 234,
        "room_name": "abc@outlook.com kotak@outlook.com",
        "timestamp": "2017-02-07T19:00:58Z",
        "unique_temp_id": "K5E6HmKQJQwSovEkFhHf",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      }
    ]
  },
  "status": 200
}
```

## Login or Register

verb :

`POST /api/v2/rest/login_or_register`

request :

```
email [string]
password [string password, optional] # password will be updated if user already exist
username [string]
avatar_url [string url, optional]
device_token [string, optional]
device_platform ["ios" or "android", optional]
```


response :

```
{
    "status": 200,
    "results": {
        "user": {
            "id": 1,
            "email": "email@qiscus.com",
            "username": "Johnny Cage",
            "avatar_url": "https://myimagebucket.com/image.jpg",
            "token": "abcde1234defgh"
        },
    }
}
```

# Webhook

Webhooks make it super easy to build on top of Qiscus SDK. They are user-defined callbacks. They are triggered by events -- in this case, messages from customers and businesses. When the event occurs, the webhook will make a call to the URI it’s configured to.

## post comment

```
{
    "type": "post_comment",
    "payload": {
        "from": {
            "id": 1,
            "email": "user1@gmail.com",
            "name": "User1",
        },
        "room": {
            "id": 1,
            "topic_id": 1,
            "type": "group", # can also be single
            "name": "ini grup",
            "participants": [
                {
                    "id": 1,
                    "email": "user1@gmail.com",
                    "username": "User1",
                    "avatar_url": "http://avatar1.jpg"
                },
                {
                    "id": 2,
                    "email": "user2@gmail.com",
                    "username": "User2",
                    "avatar_url": "http://avatar2.jpg"
                }
            ]
        },
        "message": {
            "type": "text",
            "text": "ini pesan",
            "payload": {
                # comment type specific payload
            }
        }
    }
}
```



