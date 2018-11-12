# Room
You can use this API for managing various behaviour of room

## Create room

verb:
`POST /api/v2.1/rest/create_room`

request:

```bash
room_name [string]
participants[] [array of string user_id]
creator [string user_id]
room_avatar_url [string] optional
room_options [JSON to string] optional
```

response:

```json
{
  "results": {
    "room" : {
        "room_id": "16",
        "room_name": "Group Room",
        "room_type": "group",
        "room_avatar_url": "https://myimagebucket.com/image.jpg",
        "room_options": "{}",
        "room_channel_id": ""
    }
  },
  "status": 200
}
```

## Update Room

verb:
`POST /api/v2.1/rest/update_room`

request:

```bash
room_id [string required] must be group room
room_channel_id [string optional]
room_name [string optional]
room_avatar_url [string optional]
room_options [JSON to string optional]
```

response:

```json
{
  "results": {
    "changed": true,
    "room": {
        "room_id": "16",
        "room_name": "Group Room Renamed",
        "room_type": "group", // always "group"
        "room_avatar_url": "https://myimagebucket.com/image.jpg",
        "room_options": "{\"option1\":true,\"string_option2\":\"value\"}",
        "room_channel_id": "831dfb71-1e5b-42cd-bf81-f303e6e988eb",
    }
  },
  "status": 200
}
```

## Get or create room with target

verb:
`POST /api/v2.1/rest/get_or_create_room_with_target`

request:

```bash
user_ids[] [array of string] # must contains exactly 2 user_ids
room_options [JSON to string] optional
```

response:

```json
{
  "results": {
    "room" : {
        "room_id": "17",
        "room_name": "",
        "room_type": "single",
        "room_avatar_url": "",                
        "room_options": "{}",
        "room_channel_id": ""
    }
  },
  "status": 200
}
```

## Get rooms info

verb:
`GET /api/v2.1/rest/get_rooms_info`

request:

```bash
room_ids[] [array of string]
room_channel_ids[] [array of string, optional]
```

response:

```json
{
  "results": {
    "rooms": [
      {
        "room_id": "16",
        "room_name": "My Favorite Room",
        "room_type": "group",
        "room_avatar_url": "https://myimagebucket.com/image.jpg",
        "room_options": "{}",
        "room_channel_id": "831dfb71-1e5b-42cd-bf81-f303e6e988eb",
      },
      {
        "room_id": "17",
        "room_name": "",        
        "room_type": "single",
        "room_avatar_url": "",
        "room_options": "{}",
        "room_channel_id": "",
      }
    ]
  },
  "status": 200
}

```

## Add room participants

verb:
`POST /api/v2.1/rest/add_room_participants`

request:

```bash
room_id [string] # must contains valid "group" room
user_ids[] [array of string user_ids]
```

response:

```json
{
  "results": {
    "participants_added": [
        {  
          "avatar_url": "https://myimagebucket.com/image.jpg",
          "user_id": "user1@email.com",
          "username": "Liu Kang"
        }
    ],
  },
  "status": 200
}
```

## Remove room participants

verb:
`POST /api/v2.1/rest/remove_room_participants`

request:

```bash
room_id [string] # must contains valid "group" room
user_ids [array of string user_ids]
```

response:

```json
{
  "results": {
    "participants_removed": [
        {  
          "avatar_url": "https://myimagebucket.com/image.jpg",
          "user_id": "user1@email.com",
          "username": "Liu Kang"
        }
    ],
  },
  "status": 200
}
```

## Get Room Participant
Will show list of participants in certain room

verb:
`GET /api/v2.1/rest/get_room_participants`

request:
```bash
room_id [string] required
page [int] number of page, optional
limit [int] show n data
```

response:
```json
{
    "results": {
        "participants": [
            {
                "avatar_url": "https://d1edrlpyc25xu0.cloudfront.net/kiwari-prod/image/upload/0AlS8O2rr_/1507606591-  Lina_icon.png",
                "extras": {},
                "user_id": "guest2@qiscus.com",
                "username": "Qiscus Guest2"
            },
            {
                "avatar_url": "https://d1edrlpyc25xu0.cloudfront.net/kiwari-prod/image/upload/75r6s_jOHa/1507541871-avatar-mine.png",
                "extras": {},
                "user_id": "guest@qiscus.com",
                "username": "Qiscus Demo"
            }
        ]
    },
    "status": 200
}

```

## Get User Room List

Will show maximum 20 data per page. If page parameter empty, this API will return all conversations (max 100)

verb:
`GET /api/v2.1/rest/get_user_rooms`

request:

```bash
user_id [string] required
page [int] number of page, optional
limit [int] show n data, maximum and default value is 100
room_type [string] filter by room type ("single" or "group") default will return all type
```

response when **show_participants** is false:

```json
{
    "results": {
       "meta": {
            "current_page": 1,
            "total_room": 2
        },
       "rooms": [
          {
            "room_id": "16",
            "room_name": "Group Room",
            "room_type": "group",
            "room_avatar_url": "https://myimagebucket.com/image.jpg",
            "room_options": "{}",
            "room_channel_id": "831dfb71-1e5b-42cd-bf81-f303e6e988eb"
          },
          {
            "room_id": "17",
            "room_name": "",
            "room_type": "single",
            "room_avatar_url": "https://myimagebucket.com/image.jpg",
            "room_options": "{}",
            "room_channel_id": ""
          }
        ]
    },
    "status": 200
}
```

## Get Unread Count in Rooms


verb:
`GET /api/v2.1/rest/get_unread_count`

request:

```bash
user_id [string, required]
room_ids[] [array of string]
room_channel_ids[] [array of string, optional]
```

response:

```json
{
  "results": {
    "unread_counts": [
      {
        "room_id": "16",
        "unread_count": 10,
      },
      {
        "room_id": "18",
        "unread_count": 12,
      }
    ]
  },
  "status": 200
}

```

## Get or Create Channel


verb:
`GET /api/v2.1/rest/get_or_create_channel`

request:

```bash
unique_id [string, required]
participants[] [array of string, required]
```

response:

```json
{
  "results": {
    "changed": true,
    "room": {
      "room_avatar_url": "",
      "room_channel_id": "test123",
      "room_id": "787233",
      "room_name": "test123",
      "room_options": "{}",
      "room_type": "group"
    }
  },
  "status": 200
}
```
