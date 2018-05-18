# Webhooks

Webhooks make it super easy to build on top of Qiscus SDK. They are
user-defined callbacks. They are triggered by events -- in this case, messages
from customers and businesses. When the event occurs, the webhook will
make a http(s) call to the URI it’s configured to.

## On Post Message

Webhooks on post message being triggered either from sdk client side or
from REST API

PROTOCOL : HTTPS
VERB : POST

payload being send to your endpoint is below

```json
{
    "type": "post_comment_mobile", // either type "post_comment_mobile" if from client side or "post_comment_rest" if from REST API
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
