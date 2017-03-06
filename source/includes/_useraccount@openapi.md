# OpenApi

## OpenID查询用户信息 （QueryUserNameByOpenID）

```Java
        //应用id
        String appid = "yourAppid";
        //私钥
        String clientPrivateKey = "yourPrivateKey";
        //公钥
        String serverPublicKey = "yourPublicKey";
        //初始化操作
        OpenApiClient.Init(appid, RsaCryptoHelper.PKCSType.PKCS8, serverPublicKey, clientPrivateKey);

        String accessToken = "accessToken";
        //请求url
        String url = "http://gw.open.ppdai.com/open/openApiPublicQueryService/QueryUserNameByOpenID";
        Result result = OpenApiClient.send(url, accessToken
                , new PropertyObject("Timestamp", new Date(), ValueTypeEnum.DateTime));
        //TODO rsaCryptoHelper 获取问题
        System.out.println(String.format("返回结果:%s", result.isSucess() ? OpenApiClient.getRsaCryptoHelper().decryptByPrivateKey(result.getContext()) : result.getErrorMessage()));
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
            String Url = "http://gw.open.ppdai.com/open/openApiPublicQueryService/QueryUserNameByOpenID";
            string AccessToken = "accessToken";
            Result Result = OpenApiClient.Send(Url, AccessToken
                    , new PropertyObject("Timestamp", DateTime.Now, ValueTypeEnum.DateTime));
            //TODO rsaCryptoHelper 获取问题
            RsaCryptoHelper rsaCryptoHelper = new RsaCryptoHelper(PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            string txt2 = rsaCryptoHelper.EncryptByPublicKey(Result.Context);
            Console.WriteLine(txt2);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#根据OpenID查询用户信息,其中username需要用服务器公钥解密
access_url = "http://gw.open.ppdai.com/open/openApiPublicQueryService/QueryUserNameByOpenID"
access_token = "your_access_token"
data = {
  "OpenID": "befc7084c59845b68c85917b62580a8e1"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*根据OpenID查询用户信息,其中username需要用服务器公钥解密*/
$url = "http://gw.open.ppdai.com/open/openApiPublicQueryService/QueryUserNameByOpenID";
$accessToken="yourAccessToken";
$request = '{
  "OpenID": "befc7084c59845b68c85917b62580a8e1"
}';
$result = send($url, $request,$accessToken);
echo $result
```

```Shell
curl http://gw.open.ppdai.com/account/{open_id} \
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
X-PPD-ACCESSTOKEN|	String|	是|	授权令牌	|8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
OpenID|	string|	是	|OpenID	|befc7084c59845b68c85917b62580a8e1

> 请求参数示例:

```json
    [
      {
     "OpenID": "befc7084c59845b68c85917b62580a8e1"
      }
    ]
```

### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
ReturnCode	|Int|	返回码 0=成功， -1=失败	|0
ReturnMessage	|String|	失败的消息	|
UserName	|String	|加密后的用户名称|	Cjyd2yE0+0mZl7hhAd9j/QdimtdeMH0itSQmkMrDxlLSeLwouRjsPL9jGXcXZ/PmFG6aEHa38m

> 返回值示例:

```json
[
  {
   "ReturnCode": 0,
  "ReturnMessage": null,
  "UserName": "Cjyd2yE0+0mZl7hhAd9j/QdimtdeMe0itSUD5iXdAMV0aYDOWIQmkMrDxlLSeLwouRjsPL9jGXc/zPAjoEmBuVhydSXCWwdLazW9tXwXZ/yfA86L2VcQMjaFSJo7b9We/VCbgfxL5salq8QsO29LMb0+kErZzPmFG6aEHa38mrY="
  }
]
```

### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-100007101	|OpenID不能为空	|请输入对应的OpenID
-100007302	|未查询到对应用户名|	请核对OpenID
-1	|未知异常|

> 异常示例:

```json
[
{
  "ReturnCode": -100007101,
  "ReturnMessage": "OpenID不能为空",
  "UserName": null
}
]
```

