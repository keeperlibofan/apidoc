API
```
√ /1.0/service.register // 用户注册的api
√ /1.0/service.login    // 登录的api
. /1.0/foot.recognize   // 足部识别api
. /1.0/user.addFootData // 添加脚部数据
. /1.0/user.getFootData // 获取足部数据
. /1.0/user.deleteFootData          // 删除足部数据
. /1.0/user.addAddress              // 添加地址
. /1.0/user.getAddress              // 获取地址， 返回数据的第一个就是默认地址
. /1.0/user.deleteAddress           // 根据id删除地址
x /1.0/user.addShoppingItem         // 生成购物车物品
x /1.0/user.addShoppingItem         // 删除购物车物品

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
        "expire": 1533955051,
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MzM5NTUwNTEsIm9wZW5JRCI6Im82OW54NUd1alpGZ0IyVHJaN1BSbzBsdVRENm8ifQ.63sZXboVH4PfGxLqOPg9z2OA-9M63p94ewcXImKJajg",
        "user": {
            "_id": "5b6a51e9556edf1f3d6c8577",
            "gender": 1,
            "headImg": "https://wx.qlogo.cn/mmopen/vi_32/zcFiaYibsHnfAAvVNmhiauX6wdRuCBrAvTBUso5DDMG7iaUo42rFyyclPD6ZjiaRIkvVVPQL8qPibl6m2vIiclH1fibLkA/132",
            "name": "ボー",
            "openID": "o69nx5GujZFgB2TrZ7PRo0luTD6o",
            "personalPageImg": "https://wx.qlogo.cn/mmopen/vi_32/zcFiaYibsHnfAAvVNmhiauX6wdRuCBrAvTBUso5DDMG7iaUo42rFyyclPD6ZjiaRIkvVVPQL8qPibl6m2vIiclH1fibLkA/132",
            "weixinCity": "Los Angeles City",
            "weixinCountry": "",
            "weixinNickname": "ボー",
            "weixinProvince": "California"
        }
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
POST field
```json
foot_images: Files // 第一个数据是前足，第二个数据侧足，一个field放俩张图片
direction: String
```

#### Response
json
```go
type SingleFootData struct {
	SideHeight   int			`json:"side_height"`
	Side2Tip 	 int  			`json:"side_2tip"`
	Side2heel    int 			`json:"side_2heel"`
	Length       int			`json:"length"`
	Width 		 int			`json:"width"`
	Type 		 string 		`json:"direction"`
}
```

### Add foot data

POST /1.0/user.addFootData

#### Request

```json
{
	"left": {
		"side_height": 101,
		"side_2tip": 102,
		"side_2heel":103,
		"length":104,
		"width":105
	},
	"right": {
		"side_height": 101,
		"side_2tip": 102,
		"side_2heel":103,
		"length":104,
		"width":105
	}
}
```

#### Response

>example
```json
{
    "data": String, // 这个string是创建脚数据后系统生成的id
    "error": "",
    "success": true
}
```

### Get foot data

GET /1.0/user.getFootData

#### Request

No body

#### Response

> example
```json
{
    "data": [
        {
            "_id": "5b6a84aa556edf3b840a4ba7",
            "createAt": 1533785300,
            "left": {
                "side_height": 101,
                "side_2tip": 102,
                "side_2heel": 103,
                "length": 104,
                "width": 105
            },
            "right": {
                "side_height": 101,
                "side_2tip": 102,
                "side_2heel": 103,
                "length": 104,
                "width": 105
            }
        },
        {
            "_id": "5b6bb50e556edf4f30ee0d60",
            "createAt": 1533785358,
            "left": {
                "side_height": 101,
                "side_2tip": 102,
                "side_2heel": 103,
                "length": 104,
                "width": 105
            },
            "right": {
                "side_height": 101,
                "side_2tip": 102,
                "side_2heel": 103,
                "length": 104,
                "width": 105
            }
        }
    ],
    "error": "",
    "success": true
}
```


### delete foot data

POST /1.0/user.deleteFootData

#### Introduce

根据用户足部数据的id来删除特定的足部数据

#### Request
>example
```json
{
	"_id": "5b6a84aa556edf3b840a4ba7"
}
```

#### Response

>example
```json
{
    "data": null,
    "error": "",
    "success": true
}
```

### add address

#### Introduce
添加地址

#### Request
>example
```json
{
	"name": "李博帆",
	"telNum": "15387550833",
	"province": "hunan",
	"city": "changsha",
	"country": "china",
	"detailInfo": "babababa",
	"postCode": 43011111
}
```

#### Response

>example
```
{
    "data": "5b6fc343556edf179cfa5970", // 这个就是用来删除地址的id
    "error": "",
    "success": true
}
```


### delete address

POST /1.0/user.deleteAddress

#### Request
>example

```json
{
	"_id": "5b6fc343556edf179cfa5970"
}
```

#### Response

>example
```json
{
    "data": null,
    "error": "",
    "success": true
}
```