API
```
√ /1.0/service.register             // 用户注册的api
√ /1.0/service.login                // 登录的api
. /1.0/foot.recognize               // 足部识别api
. /1.0/foot.recognize.url           // 足部识别api url方式
. /1.0/user.addFootData             // 添加脚部数据
. /1.0/user.getFootData             // 获取足部数据
. /1.0/user.deleteFootData          // 删除足部数据
. /1.0/user.addAddress              // 添加地址
. /1.0/user.getAddress              // 获取地址， 返回数据的第一个就是默认地址
. /1.0/user.deleteAddress           // 根据id删除地址
. /1.0/user.addShoppingItem         // 生成购物车物品
. /1.0/user.deleteShoppingItem      // 删除购物车物品
. /1.0/user.getShoppingItem         // 获取购物车信息
. /1.0/order.create                 // 生成订单
x /1.0/order.cancel                 // 未支付订单取消，取消后优惠码将可以继续使用
. /1.0/answerSheet.create           // 生成问卷
. /1.0/promotionCode.draw           // 抽取优惠码
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
POST /1.0/foot.recognize.url // url识别法

#### Request
POST field
```json
foot_images: Files // 第一个数据是前足，第二个数据侧足，一个field放俩张图片
direction: String
```

>example
POST
url 识别法
```json
{
	"front": "https://fitter-foot-1257227594.cos.ap-chengdu.myqcloud.com/2018-8-15/1534308626882wxbfd230984530a8d8.o6zAJs48kw6OQSPq7AWjvq14_ync.5i1N2l91gIOp290e1a37dcaa1ff3f172ef4d1376bd64.jpg",
	"side": "https://fitter-foot-1257227594.cos.ap-chengdu.myqcloud.com/2018-8-15/1534308640946wxbfd230984530a8d8.o6zAJs48kw6OQSPq7AWjvq14_ync.t1EhYQy1YTgl41f56c3cd6cd3815fefbb6072b022a25.jpg",
	"direction": "left"
}
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

### get address

GET /1.0/user.getAddress

#### Request

null

#### Response

```json
{
    "data": [
        {
            "_id": "5b6fc695556edf1abcb38400",
            "name": "李博帆",
            "telNum": "15387550833",
            "province": "hunan",
            "city": "changsha",
            "country": "china",
            "detailInfo": "babababa",
            "postCode": 43011111
        },
        {
            "_id": "5b6fc694556edf1abcb383ff",
            "name": "李博帆",
            "telNum": "15387550833",
            "province": "hunan",
            "city": "changsha",
            "country": "china",
            "detailInfo": "babababa",
            "postCode": 43011111
        },
        {
            "_id": "5b6fc690556edf1abcb383fe",
            "name": "李博帆",
            "telNum": "15387550833",
            "province": "hunan",
            "city": "changsha",
            "country": "china",
            "detailInfo": "babababa",
            "postCode": 43011111
        }
    ],
    "error": "",
    "success": true
}
```

### add shopping item

POST /1.0/user.addShoppingItem

#### Request

```json
{
	"type": "sport",   // "daily", "sport"
	"theme": "scrawl",   // "chemistry", "scrawl", "red"
	"footID": "5b6bc224556edf5d80fe7520",
	"npair": 2
}
```

#### Response

```json
{
    "data": null,
    "error": "",
    "success": true
}
```

### delete shopping item

POST /1.0/user.deleteShoppingItem

#### Request

```json
{
    index: Int     // 需要删除的数据的index
}
```

#### Response
```json
{
    "data": null,
    "error": "",
    "success": true
}
```

### get shopping items

GET /1.0/user.getShoppingItem         // 获取购物车信息

#### Request
null
#### Response
>example
```json
{
    "data": [
        {
            "type": "daily",
            "theme": "red",
            "footID": "5b6bc224556edf5d80fe7520",
            "npair": 2
        }
    ],
    "error": "",
    "success": true
}
```

### Order create

POST /1.0/order.create

#### Notice

成功请求

#### Request

> example
1. 不填优惠码
```json
{
	"promotionCode": "",
	"addressID": "5b6fc690556edf1abcb383fe"
}
```
2. 填写优惠码
```json
{
    "promotionCode"
}
```

#### Response

>example
1. 不填写优惠码
```json
{
    "data": {
        "nonceStr": "s0JjumDj7UMxsKTh",
        "package": "prepay_id=wx201120244253696dc31ea8312655009410",
        "paySign": "014CF4F5E278CED6F55139A2073D66F5",
        "signType": "MD5",
        "timeStamp": 1534735224
    },
    "error": "",
    "success": true
}
```
2. 填写优惠码

### AnswerSheet create

POST /answerSheet.create

#### Notice

问卷每个用户只能填写一次，创建问卷后，你有一次抽奖的机会，请调用抽奖的接口

#### Request
>example
```json
{
	"quiz_1": [97,98], // ASCII码 97代表'a' 传一个数组就行的 多选题
	"quiz_2": [97,98],
	"quiz_3": 97,
	"quiz_4": 97
}
```

#### Response

>example

```json
{
    "data": "5b7cd1a8556edf8052c08baa", // 问卷的id
    "error": "",
    "success": true
}
```


### promotion code draw

GET /promotionCode.draw

#### notice

打完问卷才能获得一次抽奖机会，所以说要先调用答问卷的api

#### Request

no param

#### Response

```json
{
    "data": {
        "promotionCode": "OpmVLn3bRqPP7eI3",
        "discount": 8,    // 优惠金额 单位 CNY
    },
    "error": "",
    "success": true
}
```


