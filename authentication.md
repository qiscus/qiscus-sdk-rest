# Authentication

Add `SECRET KEY` on every header's request as 'QISCUS_SDK_SECRET', you can get the value from www.qiscus.com/dashboard

so for example if your `SECRET KEY` value is `8355105e6171795fca176366e0c16f22`, your header request will be :

```bash
headers :

QISCUS_SDK_SECRET: 8355105e6171795fca176366e0c16f22
```

## Get User Authentication Token
In case you need user session token is compromised, you can get it by calling get_user_token API.

verb: `GET /api/v2.1/rest/get_user_token`

request:
```bash
user_id [string]
```

response:
```json
{
    "results": {
        "token": "abcdef09876"
    },
    "status": 200
}

```

## Reset User Authentication Token

In case your user token is compromised, you can reset their token at any time. This make previous token no longer valid.

verb:

`POST /api/v2.1/rest/reset_user_token`

request:

```bash
user_id [string] user id to reset
```

response:

```json
{
    "results": {
        "token": "qwerty12345"
    },
    "status": 200
}
```