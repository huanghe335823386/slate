# 注册相关（Register）

以下接口为用户注册相关接口

## 注册 (Register)
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
        String url = "http://gw.open.ppdai.com/auth/registerservice/register";
        Result result = OpenApiClient.send(url
                , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                , new PropertyObject("Email", "xxxxxx@ppdai.com", ValueTypeEnum.String)
                , new PropertyObject("Role", 12, ValueTypeEnum.Int32));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));
```

```.Net
//应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求url
            String Url = "http://gw.open.ppdai.com/auth/registerservice/register";
            Result Result = OpenApiClient.Send(Url
                    , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                    , new PropertyObject("Email", "xxxxxx@ppdai.com", ValueTypeEnum.String)
                    , new PropertyObject("Role", 12, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#用户注册接口，提供使用用户的手机、邮箱注册用户
access_url = "http://gw.open.ppdai.com/auth/registerservice/register"
data = {
  "Mobile": "15200000111",
  "Email": "xxxxxx@ppdai.com",
  "Role": 12
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)
```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*用户注册接口，提供使用用户的手机、邮箱注册用户*/
$url = "http://gw.open.ppdai.com/auth/registerservice/register";
$request = '{
  "Mobile": "15200000111",
  "Email": "xxxxxx@ppdai.com",
  "Role": 12
}';
$result = send($url, $request);
echo $result
```

```Shell
cur http://gw.open.ppdai.com/account/register \
-d account_name=13916818800 \
-d role=4 \
-d sign="xxx1"
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|	String|	是	|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是|	UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN	|String	|是	|使用私钥对应用ID+时间戳进行签名|
X-PPD-SIGNVERSION|	Double|	否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double|	否|	服务器版本号,最新版本号为1|	1
X-PPD-SIGN	|String	|是	|使用私钥对请求报文体进行签名|

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Mobile	|String	|否	|用户注册手机号，与邮箱中必须输入至少一项	|13911111111
Email	|String	|否	|用户注册邮箱，与用户手机至少需要输入一项	|xxxxxx@ppdai.com
Role	|Int	|是	|用户角色：借出者-4，借入者-8，借入借出者-12	|12

> 请求参数示例:

```json
    [
      {
       "Mobile": "15200000111",
  "Email": "xxxxxx@ppdai.com",
  "Role": 12
      }
    ]
```

### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
ReturnCode	|Int|	返回码	|0
ReturnMessage|	String	|返回文本信息	|用户角色信息异常
UserName	|String|	生成的用户名|	pdu8512415174
OpenID	|String|	用户在第三方平台上的唯一标识	|706762e882f94c809fa588bb262e330f
AccessToken|	String|	用户给第三方平台的授权访问令牌,有效期7天	|d70f7da0-a0e2-48cb-86a4-9a229cfce076
RefreshToken|	String	|用户给第三方授权使用刷新令牌,有效期90天	|a21b0472-41bd-4805-b3cc-ec4f792e60bf
ExpiresIn	|Int|	用户给第三方授权访问令牌超时时间，单位s。	|604799
> 返回值示例:

```json
[
 {
  "ReturnCode": 0,
  "ReturnMessage": null,
  "UserName": "pdu8512415174",
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
-1	|系统异常	|稍后重试或联系客服
-100003101	|手机和邮箱不能同时为空	|手机和邮箱请至少填一项
-100003102	|用户角色信息异常	|按照参数说明正确的填写用户角色
-100003201	|用户角色错误	|按照参数说明正确的填写用户角色
-100003202	|用户名不能为空	|稍后重试或联系客服
-100003203	|用户名格式不正确	|按照参数说明正确的填写用户角色
-100003204	|用户名已被注册	|稍后重试或联系客服
-100003205	|手机号格式不正确	|稍后重试或联系客服
-100003206	|手机号已被注册	|稍后重试或联系客服
-100003301	|AppID 验证错误	|请确认AppID或联系客服
-100003302	|用户信息错误	|输入正确的用户信息或联系客服
-100003303	|用户与App绑定失败	|稍后重试或联系客服
-100003304	|用户登录App失败	|稍后重试或联系客服
-100003401	|邮箱格式不正确	|按照说明输入正确邮箱参数
-100003402	|邮箱已被注册	|请更换邮箱并重试
> 异常示例:

```json
[
{
  "ReturnCode": -1,
  "ReturnMessage": "系统异常"
}
]
```



## 发送注册验证码(SendSMSRegisterCode)
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
        String url = "http://gw.open.ppdai.com/auth/registerservice/sendsmsregistercode";
        Result result = OpenApiClient.send(url
                , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));
}
```

```.Net
//应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求url
            String Url = "http://gw.open.ppdai.com/auth/registerservice/sendsmsregistercode";
            Result Result = OpenApiClient.Send(Url
                    , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                    , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#发送注册验证码
access_url = "http://gw.open.ppdai.com/auth/registerservice/sendsmsregistercode"
data = {
  "Mobile": "15200000001",
  "DeviceFP": "1234567890"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)
```

```PHP
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

```Shell
curl http://gw.open.ppdai.com/account/{mobile}/sendsmsregistercode \
-d devicefp="xxxff" \
-d sign="xxx1"
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|	String|	是	|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是|	UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN	|String	|是	|使用私钥对应用ID+时间戳进行签名|
X-PPD-SIGNVERSION|	Double|	否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double|	否|	服务器版本号,最新版本号为1|	1
X-PPD-SIGN	|String	|是	|使用私钥对请求报文体进行签名|

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Mobile	|String|	是	|注册手机号|	15200000001
DeviceFP|	String	|是|	设备指纹，对应设备的唯一标识	|9b8b9a1bea324e92bf00ae78d31e21e8
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
ResultCode	|Int|	返回码	|0
ResultMessage	|String|	动态注册验证码发送成功	|返回信息

> 返回值示例:

```json
[
 {
 "ResultCode": 0,
  "ResultMessage": "动态注册验证码发送成功"
}
]
```
### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-1	|内部异常	|请稍后重试或联系客服
-100004101	|设备指纹不能为空	|请输入设备指纹
-100004102	|手机号不能为空	|请输入手机号
-100004301	|当前手机已绑定有效用户	|请更换有效手机号
-100004201	|两次发送短信时间不能低于一分钟	|请稍后重试
-100004202	|一天内发送次数不能超过10次	|请稍后重试
-100004203	|动态注册验证码发送失败	|请稍后重试或联系客服
> 异常示例:

```json
[
{
   "ResultCode": -1,
  "ResultMessage": "内部异常"
}
]
```


## 手机注册验证码注册 (SMSCodeRegister)
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
        String url = "http://gw.open.ppdai.com/open/registerservice/smscoderegister";
        Result result = OpenApiClient.send(url
                , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String)
                , new PropertyObject("Code", "111111", ValueTypeEnum.String));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));
```

```.Net
 //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/open/registerservice/smscoderegister";
            Result Result = OpenApiClient.Send(Url
                    , new PropertyObject("Mobile", "15200000001", ValueTypeEnum.String)
                    , new PropertyObject("DeviceFP", "asdfasdf4asdf546asf", ValueTypeEnum.String)
                    , new PropertyObject("Code", "111111", ValueTypeEnum.String));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#手机注册验证码注册
access_url = "http://gw.open.ppdai.com/open/registerservice/smscoderegister"
data = {
  "Mobile": "15200000001",
  "DeviceFP": "1234567890",
  "Code": "111111",
  "Role": 8
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*手机注册验证码注册*/
$url = "http://gw.open.ppdai.com/open/registerservice/smscoderegister";
$request = '{
  "Mobile": "15200000001",
  "DeviceFP": "1234567890",
  "Code": "111111",
  "Role": 8
}';
$result = send($url, $request);
echo $result
```

```Shell
curl http://gw.open.ppdai.com/account/{mobile}/smscoderegister \
-d devicefp="xxxff" \
-d code=1100 \
-d role=4 \
-d sign="xxx1"
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|	String|	是	|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是|	UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN	|String	|是	|使用私钥对应用ID+时间戳进行签名|
X-PPD-SIGNVERSION|	Double|	否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double|	否|	服务器版本号,最新版本号为1|	1
X-PPD-SIGN	|String	|是	|使用私钥对请求报文体进行签名|

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
Mobile	|String	|是|	注册手机号	|15200000001
DeviceFP|	String	|是	|设备指纹，对应设备的唯一标识|	9b8b9a1bea324e92bf00ae78d31e21e8
Code	|String	|是	|验证码	|111111
Role	|Int	|否	|角色类型:4-借出,8-借入,12-借入借出	|4
> 请求参数示例:

```json
    [
     {
  "Mobile": "15200000001",
  "DeviceFP": "1234567890",
  "Code": "111111",
  "Role": 8
}
    ]
```

### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
ResultCode	|Int|	返回码|	0
ResultMessage|	String|	返回信息	|手机号不能为空
OpenID|	String	|用户在第三方平台上的唯一标识|	706762e882f94c809fa588bb262e330f
AccessToken	|String	|用户给第三方平台的授权访问令牌,有效期7天	|d70f7da0-a0e2-48cb-86a4-9a229cfce076
RefreshToken|	String	|用户给第三方授权使用刷新令牌,有效期90天	|a21b0472-41bd-4805-b3cc-ec4f792e60bf
ExpiresIn	|Int|	用户给第三方授权访问令牌超时时间，单位s	|604799
> 返回值示例:

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
-1	|系统异常	|请稍后重试或联系客服
-100005101	|设备指纹不能为空	|请输入设备指纹
-100005103	|手机号不能为空	|请输入手机号
-100005302	|平台信息错误	|请稍后重试或联系客服
-100005303	|授权失败	|请稍后重试或联系客服
-100005202	|验证码输入错误次数太多，请稍后重试	|请稍后重试
-100005201	|验证码输入错误	|请输入正确的验证码
-100005301	|注册失败	|请稍后重试或联系客服
-100005102	|验证码不能为空	|请输入动态验证码
-100005104	|角色信息错误	|输入正确的角色类型
> 异常示例:

```json
[
{
   "ResultCode": -1,
  "ResultMessage": "内部异常"
}
]
```


## 验证帐号是否存在 (AccountExist)
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
        String url = "http://gw.open.ppdai.com/auth/registerservice/accountexist";
        Result result = OpenApiClient.send(url
                , new PropertyObject("AccountName", "15200000001", ValueTypeEnum.String));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```.Net
 //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/auth/registerservice/accountexist";
            Result Result = OpenApiClient.Send(Url
                    , new PropertyObject("AccountName", "15200000001", ValueTypeEnum.String));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#验证帐号是否存在
access_url = "http://gw.open.ppdai.com/auth/registerservice/accountexist"
data = {
  "AccountName": "15200000001"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*验证帐号是否存在*/
$url = "http://gw.open.ppdai.com/auth/registerservice/accountexist";
$request = '{
  "AccountName": "15200000001"
}';
$result = send($url, $request);
echo $result
```

```Shell
curl http://gw.open.ppdai.com/account/check/{accountname} \
-d sign="xxx1"
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|	String|	是	|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是|	UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN	|String	|是	|使用私钥对应用ID+时间戳进行签名|
X-PPD-SIGNVERSION|	Double|	否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double|	否|	服务器版本号,最新版本号为1|	1
X-PPD-SIGN	|String	|是	|使用私钥对请求报文体进行签名|

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
AccountName|	String	|是	|帐号名称,支持手机\邮箱\自定义帐号	|15200000001

> 请求参数示例:

```json
    [
     {
  "AccountName": "15200000001"
}
    ]
```


### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
ResultCode	|Int|	返回码	|0
ResultMessage|	String	|返回信息|	内部异常
IsExist|	Boolean	|帐号是否存在|	true
> 返回值示例:

```json
[
{
  "ResultCode": 0,
  "ResultMessage": null,
  "IsExist": true
}
]
```
### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-1	|内部异常	|请稍后重试或联系客服
> 异常示例:

```json
[
{
   "ResultCode": -1,
  "ResultMessage": "内部异常"
}
]
```

