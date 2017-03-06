# 登录相关（AuthLogin）

以下接口为用户登录相关接口

## 发送登录动态密码 (SendSMSAuthCode)

```Java
//应用id
String appid = "yourappid";
//私钥
String clientPrivateKey = "yourclientprovatekey";
//公钥
String serverPublicKey = "publickey";
//请求url
String url = "http://gw.open.ppdai.com/auth/authservice/sendsmsauthcode";
try {
    OpenApiClient.Init(appid, RsaCryptoHelper.PKCSType.PKCS8, serverPublicKey, clientPrivateKey);
    Result result = OpenApiClient.send(url
            , new PropertyObject("Mobile", "13900000000", ValueTypeEnum.String)
            , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String));
    System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));
} catch (Exception e) {
    e.printStackTrace();
}
```

```csharp
//应用id
string Appid = "yourAppid";
//私钥
string ClientPrivateKey = "yourPrivateKey";
//公钥
string ServerPublicKey = "yourPublicKey";
//请求Url
string Url = "http://gw.open.ppdai.com/auth/authservice/sendsmsauthcode";
OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
Result Result = OpenApiClient.Send(Url, new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String), new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String));
Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
access_url = "http://gw.open.ppdai.com/auth/registerservice/sendsmsregistercode"
data = {
  "Mobile": "15200000001",
  "DeviceFP": "1234567890"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)
```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*发送注册验证码*/
$url = "http://gw.open.ppdai.com/auth/registerservice/sendsmsregistercode";
$request = '{
  "Mobile": "15200000001",
  "DeviceFP": "1234567890"
}';
$result = send($url, $request);
echo $result
```

```shell
curl http://gw.open.ppdai.com/account/{mobile}/sendsmsregistercode \
-d devicefp="xxxff" \
-d sign="xxx1"
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID	|String	|是|	拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP|	String|	是	|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN | String	|是	|使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION	|Double|	否	|签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION |  Double |	否	服务器版本号,最新版本号为1	|1
X-PPD-SIGN	String	|是	|使用私钥对请求报文体进行签名|


### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Mobile|String|是|登录手机号	|15200000001
DeviceFP|String	|是	|设备指纹，对应设备的唯一标识|	9b8b9a1bea324e92bf00ae78d31e21e8

> 请求参数示例:

```json
    [
      {
      "Mobile": "15200000001",
      "DeviceFP": "1234567890"
      }
    ]
```

### Response Parameters
参数 | 类型 | 描述| 示例值

--------- |  -----------|---------|-------
ResultCode|	Int|	0	|返回码
ResultMessage|	String|	返回信息	|动态注册验证码发送成功

> 返回值示例:

```json
[
  {
    "ResultCode": 0,
    "ResultMessage": "动态登录密码发送成功"
  }
]
```

### ERROR CODE DESCRIPTION

名称|	描述|	解决方案
--------- | ------- | -----------
-1|	内部异常	|请稍后重试或联系客服
-100001101	|设备指纹不能为空	|请输入设备指纹
-100001102	|手机号不能为空	|请输入手机号
-100001201	|当前手机未绑定有效用户	|请更换有效手机号
-100001202	|两次发送短信时间间隔不能低于一分钟	|请稍后重试
-100001203	|一天内发送次数不能超过10次	|请稍后重试
-100001204	|动态登录密码发送失败	|请稍后重试或联系客服
-100001205	|已注销，请联系客服	|请联系客服
> 异常示例:

```json
[
  {
    "ResultCode": -1,
    "ResultMessage": "内部异常"
  }
]
```



## 手机动态密码登录(SMSAuthCodeLogin)

```Java
        //应用id
        String appid = "yourAppid";
        //私钥
        String clientPrivateKey = "yourPrivateKey";
        //公钥
        String serverPublicKey = "yourPublicKey";
        //初始化操作
        OpenApiClient.Init(appid, RsaCryptoHelper.PKCSType.PKCS8, serverPublicKey, clientPrivateKey);

        //请求url
        String url = "http://gw.open.ppdai.com/open/oauthservice/smsauthcodelogin";
        Result result = OpenApiClient.send(url
                , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String)
                , new PropertyObject("SMSAuthCode", "111111", ValueTypeEnum.String));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));
```

```csharp
//应用id
string Appid = "yourAppid";
//私钥
string ClientPrivateKey = "yourPrivateKey";
//公钥
string ServerPublicKey = "yourPublicKey";
//请求Url
string Url = "http://gw.open.ppdai.com/auth/authservice/sendsmsauthcode";
OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
Result Result = OpenApiClient.Send(Url
                , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String)
                , new PropertyObject("SMSAuthCode", "111111", ValueTypeEnum.String));
Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
access_url = "http://gw.open.ppdai.com/open/oauthservice/smsauthcodelogin"
data = {
  "Mobile": "15200000001",
  "DeviceFP": "1234567890",
  "SMSAuthCode": "111111"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)
```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
$url = "http://gw.open.ppdai.com/open/oauthservice/smsauthcodelogin";
$request = '{
  "Mobile": "15200000001",
  "DeviceFP": "1234567890",
  "SMSAuthCode": "111111"
}';
$result = send($url, $request);
echo $result

```

```shell
curl http://gw.open.ppdai.com/open/oauthservice/smsauthcodelogin \
-d devicefp="xxxff" \
-d sign="xxx1"
```

### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID	|String	是	|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是	|UTC时间戳|	yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN|	String	|是	|使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION|	Double	|否	|签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION|	Double|	否	|服务器版本号,最新版本号为1|	1
X-PPD-SIGN	|String	|是|	使用私钥对请求报文体进行签名|
### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Mobile|	String	|是	|注册手机号|	15200000001
DeviceFP|	String	|是|	设备指纹，对应设备的唯一标识	|9b8b9a1bea324e92bf00ae78d31e21e8
SMSAuthCode|	String|	是	|动态登录密码	|111111

> 请求参数示例:

```json
    [
      {
      "Mobile": "15200000001",
  "DeviceFP": "1234567890",
  "SMSAuthCode": "111111"
      }
    ]
```

### Response Parameters

参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
ResultCode|	Int|	返回码	|0
ResultMessage|	String|	返回信息|	手机号不能为空
RefreshToken|	String	|用户给第三方授权使用刷新令牌,有效期90天|	a21b0472-41bd-4805-b3cc-ec4f792e60bf
ExpiresIn	|Int|	用户给第三方授权访问令牌超时时间，单位s|	604799
OpenID|	String	|用户在第三方平台上的唯一标识	|706762e882f94c809fa588bb262e330f
AccessToken|	String|	用户给第三方平台的授权访问令牌,有效期7天|	d70f7da0-a0e2-48cb-86a4-9a229cfce076

```json
[
  {
    "ReturnCode": 0,
  "ReturnMessage": null,
  "OpenID": "706762e882f94c809fa588bb262e330f",
  "AccessToken": "d70f7da0-a0e2-48cb-86a4-9a229cfce076",
  "RefreshToken": "a21b0472-41bd-4805-b3cc-ec4f792e60bf",
  "ExpiresIn": 604799
  }
]
```

### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-1	|内部异常	请稍后重试或联系客服
-100002101|	设备指纹不能为空|	请输入设备指纹
-100002102|	手机号不能为空	|请输入手机号
-100002103|	动态登录密码不能为空	|请输入动态登录密码
-100002301	|用户手机不存在	|请稍后重试或联系客服
-100002401|	平台信息错误	|请稍后重试或联系客服
-100002402|	授权失败	|请稍后重试或联系客服
-100002202|	动态密码输入错误	|请输入正确的动态密码
-100002201|	验证码不能为空	|请输入动态验证码密码

> 异常示例:

```json
[
  {
    "ResultCode": -1,
    "ResultMessage": "内部异常"
  }
]
```

## 自动登录接口（AutoLogin）

```Java
//应用id
String appid = "yourappid";
//私钥
String clientPrivateKey = "yourclientprovatekey";
//公钥
String serverPublicKey = "publickey";
//请求url
String url = "http://gw.open.ppdai.com/auth/LoginService/AutoLogin";
try {
    OpenApiClient.Init(appid, RsaCryptoHelper.PKCSType.PKCS8, serverPublicKey, clientPrivateKey);
    Result result = OpenApiClient.send(url
            , new PropertyObject("Mobile", "13900000000", ValueTypeEnum.String)
            , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String));
    System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));
} catch (Exception e) {
    e.printStackTrace();
}
```

```csharp
//应用id
string Appid = "yourAppid";
//私钥
string ClientPrivateKey = "yourPrivateKey";
//公钥
string ServerPublicKey = "yourPublicKey";
//请求Url
string Url = "http://gw.open.ppdai.com/auth/LoginService/AutoLogin";
OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
Result Result = OpenApiClient.Send(Url, new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String), new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String));
Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
access_url = "http://gw.open.ppdai.com/auth/LoginService/AutoLogin"
data = {
  "Mobile": "15200000001",
  "DeviceFP": "1234567890"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)
```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*发送注册验证码*/
$url = "http://gw.open.ppdai.com/auth/LoginService/AutoLogin";
$request = '{
  "Mobile": "15200000001",
  "DeviceFP": "1234567890"
}';
$result = send($url, $request);
echo $result
```

```shell
curl http://gw.open.ppdai.com/auth/LoginService/AutoLogin \
-d devicefp="xxxff" \
-d sign="xxx1"
```

### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID	|String	|是|	拍拍贷分配给开发者的应用Id|	9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是	|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN	|String|	是|	使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION	|Double|	否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double	|否|	服务器版本号,最新版本号为1	|1
X-PPD-SIGN|	String|	是|	使用私钥对请求报文体进行签名	|
X-PPD-ACCESSTOKEN|	String|	是	|授权令牌|	8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Timestamp	|DateTime	|是	|时间戳	|2016-03-14 19:15:22

> 请求参数示例:

```json
    [
      {
     "Timestamp": "2016-03-14 19:15:22"
      }
    ]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
ResultCode|	Int	|返回码|	0
ResultMessage|	String|	返回文本信息|	处理信息
Token	|String|	AC.PPDAI.COM自动登录用的Token,有效时间180秒	|7RH28R2MRV54
UserName|	String	|生成的用户名	|pdu8512415174

> 返回值示例:

```json
[
  {
   "ResultCode": 0,
  "ResultMessage": "登录成功",
  "Token": "7RH28R2MRV54",
  "UserName": "ppd测试用户"
  }
]
```

### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-1|	系统异常|	稍后重试或联系客服
-100006301|	登录用户信息不存在|	请核对Request.Head中的参数是否正确

> 异常示例:

```json
[
{
  "ResultCode": -1001,
  "ResultMessage": "系统异常"
}
]
```

