# Data Backup and Import

## Create or Request Backup

description: will request a backup as json
verb:
`POST /api/v2.1/rest/exports`

request:

```bash
type [string] type of resource which will be exported, permitted value are: "users", "rooms", "comments" 
start_date [string] using format "YYYY-MM-DD"
end_date [string] using format "YYYY-MM-DD" 
```

response:

```json
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

## Get List of Backup

verb:
`GET /api/v2.1/rest/exports`

request:

```bash
page [int] page number, optional
```

response:
will return maximum 20 rows of recent backup

```json
{
  "results": {
    "backup_histories": [
      {
        "created_at": "2017-07-17T10:10:57+07:00",
        "download_url":
          "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
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

## Get Backup By Id

verb:
`GET /api/v2.1/rest/exports/:backup_unique_id`
where `:backup_unique_id` is unique id of backup
response:

```json
{
  "results": {
    "backup_history": {
      "created_at": "2017-07-17T10:10:57+07:00",
      "download_url":
        "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
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

 Delete Backup By Id

verb:
`DELETE /api/v2.1/rest/exports/:backup_unique_id`

where `:backup_unique_id` is unique id of backup

response:

```json
{
  "results": {
    "backup_history": {
      "created_at": "2017-07-17T10:10:57+07:00",
      "download_url":
        "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
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

## Make an Import

verb:
`POST /api/v2.1/rest/imports`

request:

```bash
type [string] type of resource which will be exported, permitted value are: "users", "rooms", "comments"
file [file] json file, limit 4 MB each import
```

response:

```json
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

** Users **
Email and authentication token must be unique, and you must have no same
data (both email or unique id)in your database right now (you can check it
by export it first).. Password in this json is plain password and system
will encrypted it when save to db. We encourage you to use https version
of avatar url. Another key will discarded when import.

```json
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

** Rooms **

* Unique id must be unique at application level (you cannot insert a new
  data with same unique id AND application id), and you must have no same
  unique id in your database right now (you can check it by export it first).
* Avatar URL should be https.
* If room type is single, the name inserted into db will be
  changed by logic using template “partcicipant1_email {space}
  participant2_email“, so please to make sure that if your room type is single,
  your participant must contains exactly 2 participant AND one of that
  participant is specified at CreatorEmail. Otherwise, if room type is group,
  Name will be the name of group.
* CreatorEmail and all of ParticipantEmails must be exists in database
  (check by make an export users first).

```json
[
  {
    "Name": "demo1@linkdokter.com 4992614d-9d32-4cc4-ae8e-310a7a0fdbb9",
    "Type": "single",
    "Options": "",
    "CreatorEmail": "user@mymail.com",
    "CreatedAt": "2017-05-11T06:35:27Z",
    "AvatarUrl": "",
    "UniqueId": "f82e5262-e9c4-4b7b-867a-ea890ba64f43",
    "ParticipantEmails": ["user@mymail.com", "mymail@mymail.com"]
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

** Comments **

* UniqueId must be unique, and you must have no same unique id in your database
  right now (you can check it by export it first).
* RoomUniqueId must be exists in database (check by export it first).
* CreatorEmail must be exists in database.
* We remind you to only import comment using type **text **or **reply** only,
  since custom format may not fully supported.

Since comment has multiple type with different payload (and it must passes an
validator for each type), you must specify a correct payload. You may notice
that for some type, you need to pass an exact value, for example is
replied_comment_id in type reply, it can be tricky since we cannot get exact
value to get which comment id should be referred (because payload is saved
in **JSON** data type and it **cannot be related to any foreign key**). But,
thanks to RDBMS which can handle this problem. For type **reply **you must
specify a value ParentCommentUniqueId, it can be related to comment unique
id that already exist in database or UniqueId that you are specify before
current object data.

> You can refer payload format in post comment section.

Tips for import comment:
Type: reply
**text**: same as message
**replied_comment_id**: 1, you must type literally integer 1 number, since it is means true when it came to validator service.

```json
{
  "text": "ini comment",
  "replied_comment_id": 1
}
```

Example data to import:

```json
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

## Get Imported List

verb:
`GET /api/v2.1/rest/imports`
request:

```bash
page [int] page number, optional
```

response:

```json
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
