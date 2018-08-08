API
```
√ /1.0/service.register // 用户注册的api
√ /1.0/service.login    // 登录的api
. /1.0/foot.recognize   // 足部识别api
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
        "_id": "5b6a51e9556edf1f3d6c8577",
        "openID": "o69nx5GujZFgB2TrZ7PRo0luTD6o",
        "name": "ボー",
        "weixinNickname": "ボー",
        "headImg": "https://wx.qlogo.cn/mmopen/vi_32/zcFiaYibsHnfAAvVNmhiauX6wdRuCBrAvTBUso5DDMG7iaUo42rFyyclPD6ZjiaRIkvVVPQL8qPibl6m2vIiclH1fibLkA/132",
        "personalPageImg": "https://wx.qlogo.cn/mmopen/vi_32/zcFiaYibsHnfAAvVNmhiauX6wdRuCBrAvTBUso5DDMG7iaUo42rFyyclPD6ZjiaRIkvVVPQL8qPibl6m2vIiclH1fibLkA/132",
        "gender": 1,
        "weixinCity": "Los Angeles City",
        "weixinProvince": "California",
        "weixinCountry": ""
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

### Foot recognize

POST /1.0/foot.recognize

#### Request



#### Response