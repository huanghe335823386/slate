---
title: PPDAI API Reference

language_tabs:
  - Java
  - .net

toc_footers:
  - Copyright Reserved 2007-2016拍拍贷
  - 上海拍拍贷金融信息服务有限公司
  - 沪ICP备05063398号

includes:
  - errors

search: true
---

# 账号类
## AuthService.SendSMSAuthCode
发送登录动态密码
> 示例代码:

```Java
    java code
```

```.net
    .net code
```

> 请求参数示例:
```json
    [
      {
        "Mobile": "15200000001",
        "DeviceFP": "1234567890"
      }
    ]
```

> 返回值示例:

```json
[
  {
    "ResultCode": 0,
    "ResultMessage": "动态登录密码发送成功"
  }
]
```
> 异常示例:

```json
[
  {
    "ResultCode": -1,
    "ResultMessage": "内部异常"
  }
]
```


### HTTP Request

POST http://gw.open.ppdai.com/auth/authservice/sendsmsauthcode

### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID	String	|是|	拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	String|	是	|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN | String	|是	|使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION	|Double|	否	|签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION |  Double |	否	服务器版本号,最新版本号为1	|1
X-PPD-SIGN	String	|是	|使用私钥对请求报文体进行签名|

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Mobile|String|是|登录手机号	|15200000001
DeviceFP|String	|是	|设备指纹，对应设备的唯一标识|	9b8b9a1bea324e92bf00ae78d31e21e8

### Response Parameters
参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
ResultCode|	Int|	0	|返回码
ResultMessage|	String|	返回信息	|动态注册验证码发送成功
### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------|---------|-------
-1|	内部异常	|请稍后重试或联系客服
-100001101	|设备指纹不能为空	|请输入设备指纹
-100001102	|手机号不能为空	|请输入手机号
-100001201	|当前手机未绑定有效用户	|请更换有效手机号
-100001202	|两次发送短信时间间隔不能低于一分钟	|请稍后重试
-100001203	|一天内发送次数不能超过10次	|请稍后重试
-100001204	|动态登录密码发送失败	|请稍后重试或联系客服
-100001205	|已注销，请联系客服	|请联系客服

# 资金类

> 示例代码:

```Java
    java code
```

```.net
    .net code
```



# CPS

## BdRegService.UserInfoAdd
用户信息添加.
> 示例代码:

```Java
    java code
```

```.net
    .net code
```

> 请求参数示例:
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


### HTTP Request

POST http://gw.open.ppdai.com/cps/BdRegService/UserInfoAdd

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
--------- | ------- | -----------|---------|-------
PlatformType|	Int|	是|	平台类型1：PC; 2:移动	|2
Info|	String|	否	|用户额外的详细信息 （可选）JSON格式	|
OrderId	|String	|否	|订单号（可选） - 这个用户的唯一标志，例如：用户ID	|123456465465
SourceId|	Int	|否	|	|0

### Response Parameters
参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Result|	Int	|返回码 0=成功， 1=失败	|0
ResultCode|	String|	暂时没用到	|
ResultMessage|	string|	失败的消息	|
Content	String|	RedirectUrl |表示要跳转的地址 (需要Url解码一下)	|{"RedirectUrl":""}

<aside class="success">
    备注 — 备注备注备注备注备注备注备注备注
</aside>

#借出类

