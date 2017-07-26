# REST API

BASE_URL : [APP_ID].qiscus.com

example : if your APP_ID is `domino-prod` means the base_url will be `domino-prod.qiscus.com`

## Authentication

Add `QISCUS_SDK_SECRET` on every header's request, you can get the value from dashboard.qiscus.com

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

# Post System Event Message
To send event system message such as creating group, join room, remove member, etc

verb:

`POST /api/v2/rest/post_system_event_message`


request:

```
system_event_type [string] valid value is: "create_room", "add_member", "join_room", "remove_member", "left_room", "change_room_name", "change_room_avatar"

room_id [integer] required, room id to post

subject_email [string] required, person who create a room, add member to room, join room, remove member from room, left from room, change room name and/or room avatar

object_email[] [array of string] optional, only required when system event type is add_member or remove_member

updated_room_name [string] optional, only required when system event message type is change_room_name or create_room

```

response:
Will return last inserted comment and object id when type is add_member or remove_member.


```
{
    "results": {
        "comment": {
            "comment_before_id": 17974,
            "disable_link_preview": false,
            "email": "system@dragongo.qiscus.com",
            "id": 17975,
            "message": "Yusuf joined room",
            "payload": {
                "object_email": "",
                "object_username": "",
                "room_name": "Test Group",
                "subject_email": "userid_846_6285868233422@dragongo.com",
                "subject_username": "Yusuf",
                "type": "join_room"
            },
            "room_id": 2427,
            "timestamp": "2017-06-22T02:10:29Z",
            "topic_id": 2427,
            "type": "system_event",
            "unique_temp_id": "AOpM0LdZULDb8gw82ui3",
            "unix_timestamp": 1498097429,
            "user_avatar": {
                "avatar": {
                    "url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png"
                }
            },
            "user_avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
            "user_id": 2905,
            "username": "System"
        }
    },
    "status": 200
}
```


# Create or Request Backup

description: will request a backup as json

verb:

`POST /api/v2/rest/exports`

request:

```
type [string] type of resource which will be exported, permitted value are: "users", "rooms", "comments" 
start_date [string] using format "YYYY-MM-DD"
end_date [string] using format "YYYY-MM-DD"
```

response:

```
{
    "results": {
        "created_at": "2017-07-17T10:19:44+07:00",
        "download_url": "",
        "error_message": "",
        "original_filename": "2017-07-17T10:19:44+07:00_exported_comments.json",
        "percentage": 0,
        "resource_name": "comments",
        "size": 0,
        "status": "started",
        "total_rows": 0,
        "unique_id": "dd2c46a8-0921-4b75-837c-cee1b9804787"
    },
    "status": 200
}


```


# Get List of Backup

verb:

`GET /api/v2/rest/exports`


request:

```
page [int] page number, optional
```


response:

will return maximum 20 rows of recent backup

```
{
    "results": {
        "backup_histories": [
            {
                "created_at": "2017-07-17T10:10:57+07:00",
                "download_url": "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
                "error_message": "",
                "original_filename": "2017-07-17T10:10:57+07:00_exported_comments.json",
                "percentage": 100,
                "resource_name": "comments",
                "size": 43044263,
                "status": "finished",
                "total_rows": 119963,
                "unique_id": "c44c4168-0b45-4ac2-8942-a4f1af987a13"
            }
        ]
    },
    "status": 200
}


```


# Get Backup By Id

verb:

`GET /api/v2/rest/exports/:backup_unique_id`

where `:backup_unique_id` is unique id of backup


response:

```
{
    "results": {
        "backup_history": {
            "created_at": "2017-07-17T10:10:57+07:00",
            "download_url": "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
            "error_message": "",
            "original_filename": "2017-07-17T10:10:57+07:00_exported_comments.json",
            "percentage": 100,
            "resource_name": "comments",
            "size": 43044263,
            "status": "finished",
            "total_rows": 119963,
            "unique_id": "c44c4168-0b45-4ac2-8942-a4f1af987a13"
        }
    },
    "status": 200
}
```


# Delete Backup By Id

verb:

`DELETE /api/v2/rest/exports/:backup_unique_id`

where `:backup_unique_id` is unique id of backup


response:

```
{
    "results": {
        "backup_history": {
            "created_at": "2017-07-17T10:10:57+07:00",
            "download_url": "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
            "error_message": "",
            "original_filename": "2017-07-17T10:10:57+07:00_exported_comments.json",
            "percentage": 100,
            "resource_name": "comments",
            "size": 43044263,
            "status": "finished",
            "total_rows": 119963,
            "unique_id": "c44c4168-0b45-4ac2-8942-a4f1af987a13"
        }
    },
    "status": 200
}
```



# Make an Import

verb:

`POST /api/v2/rest/imports`


request:


```
type [string] type of resource which will be exported, permitted value are: "users", "rooms", "comments" 
file [file] json file, limit 4 MB each import
```


response:

```
{
    "results": {
        "backup_history": {
            "created_at": "2017-07-24T16:38:14+07:00",
            "errors": {
                "Message": "",
                "Data": null
            },
            "original_filename": "comment_single.json",
            "resource_name": "comments",
            "size": 926,
            "status": "started",
            "total_rows": 0,
            "unique_id": "13c4952f-4b77-4705-9523-7ddca9c45967"
        }
    },
    "status": 200
}
```

> Note: for each type, it must follows required format as specified below:


## Users

Email and authentication token must be unique, and you must have no same data (both email or unique id)in your database right now (you can check it by export it first).. Password in this json is plain password and system will encrypted it when save to db. We encourage you to use https version of avatar url. Another key will discarded when import.


```
[
  {
    "Email": "mymail@mymail.com",
    "Name": "Nama",
    "AvatarUrl": "https://placehold.it/20x20",
    "AuthenticationToken": "randomstring",
    "Password": "password",
    "CreateAt": "2017-05-10T11:46:30Z"
  }
]
```

## Rooms

* Unique id must be unique at application level (you cannot insert a new data with same unique id AND application id), and you must have no same unique id in your database right now (you can check it by export it first).
* Avatar URL should be https.
* If room type is single, the name inserted into db will be changed by logic using template “partcicipant1_email <<space>> participant2_email“, so please to make sure that if your room type is single, your participant must contains exactly 2 participant AND one of that participant is specified at CreatorEmail. Otherwise, if room type is group, Name will be the name of group.
* CreatorEmail and all of ParticipantEmails must be exists in database (check by make an export users first).


```
[
  {
    "Name": "demo1@linkdokter.com 4992614d-9d32-4cc4-ae8e-310a7a0fdbb9",
    "Type": "single",
    "Options": "",
    "CreatorEmail": "user@mymail.com",
    "CreatedAt": "2017-05-11T06:35:27Z",
    "AvatarUrl": "",
    "UniqueId": "f82e5262-e9c4-4b7b-867a-ea890ba64f43",
    "ParticipantEmails": [
      "user@mymail.com",
      "mymail@mymail.com"
    ]
  },
  {
    "Name": "Qiscus Family Super",
    "Type": "group",
    "Options": "",
    "CreatorEmail": "user@mymail.com",
    "CreatedAt": "2017-05-11T06:35:27Z",
    "AvatarUrl": "",
    "UniqueId": "f82e5262-e9c4-4b7b-867a-ea890ba64f43",
    "ParticipantEmails": [
      "user@mymail.com",
      "mymail@mymail.com",
      "newuser@mymail.com"
    ]
  }
]
```


## Comments

* UniqueId must be unique, and you must have no same unique id in your database right now (you can check it by export it first).
* RoomUniqueId must be exists in database (check by export it first).
* CreatorEmail must be exists in database.
* We remind you to only import comment using type **text **or **reply** only, since custom format may not fully supported.


Since comment has multiple type with different payload (and it must passes an validator for each type), you must specify a correct payload. You may notice that for some type, you need to pass an exact value, for example is replied_comment_id in type reply, it can be tricky since we cannot get exact value to get which comment id should be referred (because payload is saved in **JSON** data type and it **cannot be related to any foreign key**). But, thanks to RDBMS which can handle this problem. For type **reply **you must specify a value ParentCommentUniqueId, it can be related to comment unique id that already exist in database or UniqueId that you are specify before current object data.

> You can refer payload format in post comment section.


Tips for import comment:

Type: reply
**text**: same as message
**replied_comment_id**: 1, you must type literally integer 1 number, since it is means true when it came to validator service.

```
{
    "text": "ini comment",
    "replied_comment_id": 1
}
```


Example data to import:

```
[
    {
        "Message": "Halo doc",
        "DisableLinkPreview": false,
        "Type": "text",
        "UniqueId": "android_14945300625232b81ffc0520f961",
        "CreatorEmail": "userid_844_6285868233422@kiwari-stag.com",
        "RoomUniqueId": "4e6c208b-3436-46a0-a6d7-add9b90dfc77",
        "CreatedAt": "2017-05-11T19:14:24Z",
        "Payload": null,
        "ParentCommentUniqueId": ""
    },
    {
        "Message": "Maaf mau tanya..",
        "DisableLinkPreview": false,
        "Type": "reply",
        "UniqueId": "android_14945300625232b81ffc0520f962",
        "CreatorEmail": "userid_844_6285868233422@kiwari-stag.com",
        "RoomUniqueId": "4e6c208b-3436-46a0-a6d7-add9b90dfc77",
        "CreatedAt": "2017-05-11T19:14:24Z",
        "Payload": {
            "text": "Maaf mau tanya..",
            "replied_comment_id": 1
        },
        "ParentCommentUniqueId": "android_14945300625232b81ffc0520f961"
      }
]
```


# Get Imported List

verb:

`GET /api/v2/rest/imports`

request:

```
page [int] page number, optional
```

response:

```
{
    "results": {
        "backup_histories": [
            {
                "created_at": "2017-07-24T16:34:57+07:00",
                "errors": {},
                "original_filename": "comment_single.json",
                "resource_name": "comments",
                "size": 926,
                "status": "finished",
                "total_rows": 1,
                "unique_id": "85cfa162-f8ac-4e91-a6a4-a2e4ab25e150"
            }
        ]
    },
    "status": 200
}
```
