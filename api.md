API
```
√ /1.0/service.register // 用户注册的api
√ /1.0/service.login    // 登录的api
```


### register

POST /1.0/service.register

#### Introduce

用户注册的api

#### Request

Params:

```
{
	encryptedData: String,
	iv:    String,
	code:  String
}
```

#### Reponse
>example
```json

```

### login

POST /1.0/service.login

#### Introduce

用户登录的api

#### Request

Params:
```
{
    jsCode: String
}
```

#### Response

>example
```json
{
    "data": {
        "expire": 1530865482, // 过期的时间戳
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MzA4NjU0ODIsIm9wZW5JRCI6Im9Mb0VZNDJwTEJOR1p5eEpfNHlBMTZuNkpWOFUifQ.Cf-e2uvtn27DJSs7Ufxilxsn6P2ddDgI_irZ3Qi8e84",
        "user": {},
    },
    "error": "",
    "success": true
}
```

***For all following API***, Auth info(token return by login API) must be contained in HTTP header like this:
认证信息(登录api返回的token) 必须被包含在HTTP请求头中像下面这样：
```
Authorization: Bearer <token>
```

