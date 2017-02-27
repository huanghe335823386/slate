---
title: API Reference

language_tabs:
  - Java
  - .net

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# 账号类

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# 资金类

> To authorize, use this code:

```Java
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```.net
import kittn

api = kittn.authorize('meowmeowmeow')
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# CPS

## BdRegService.UserInfoAdd

```Java
    ```json
    [
      {
        "SourceId": 0,
        "PlatformType": 2,
        "Info": "{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房，目前无房贷','chechan':'有车，但是有车贷未还清','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水 10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}",
        "OrderId": "5765465456423465"
      }
    ]
    ```

```

```.Net
    ```json
        [
          {
            "SourceId": 0,
            "PlatformType": 2,
            "Info": "{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房，目前无房贷','chechan':'有车，但是有车贷未还清','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水 10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}",
            "OrderId": "5765465456423465"
          }
        ]
    ```
```

> 返回值示例:

```json
[
  {
    "Result": 0,
    "ResultCode": "null",
    "ResultMessage": "",
    "Content": {
      "RedirectUrl": "http://www.ppdai.com/......."
    }
  }
]
```

用户信息添加.

### HTTP Request

`GET http://gw.open.ppdai.com/cps/BdRegService/UserInfoAdd

### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|String|是|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP|String|是|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN|	String|	是	|使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION|	Double	|否	|签名验证版本号,最新版本号为1|	1
X-PPD-SERVICEVERSION|	Double|	否	|服务器版本号,最新版本号为1	|1
X-PPD-SIGN|	String	是|	使用私钥对请求报文体进行签名|
X-PPD-ACCESSTOKEN|	String|	是|	授权令牌|	8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
PlatformType|	Int|	是|	平台类型1：PC; 2:移动	|2
Info|	String|	否	|用户额外的详细信息 （可选）JSON格式	|
OrderId	|String	|否	|订单号（可选） - 这个用户的唯一标志，例如：用户ID	|123456465465
SourceId|	Int	|否	|	|0

### Response Parameters
参数 | 类型 | 必填 | 描述| 示例值
Result|	Int	|返回码 0=成功， 1=失败	|0
ResultCode|	String|	暂时没用到	|
ResultMessage|	string|	失败的消息	|
Content	String|	RedirectUrl |表示要跳转的地址 (需要Url解码一下)	|{"RedirectUrl":""}

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>


## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

#借出类

