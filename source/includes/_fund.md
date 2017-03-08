# 资金
资金查询接口

## 获取用户资金余额 QueryBalance

```java
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
    String url = "http://gw.open.ppdai.com/balance/balanceService/QueryBalance";
    Result result = OpenApiClient.send(url, accessToken);
    System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```csharp
    //应用id
    string Appid = "yourAppid";
    //私钥
    string ClientPrivateKey = "yourPrivateKey";
    //公钥
    string ServerPublicKey = "yourPublicKey";

    OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
    string AccessToken = "accessToken";
    //请求url
    String Url = "http://gw.open.ppdai.com/balance/balanceService/QueryBalance";
    Result Result = OpenApiClient.Send(Url, AccessToken);
    Console.WriteLine(Result);
```

```python
    appid="a769b53eb26849eba5d5e81ccb381a32"
    code = "5ae2ee0d135b47ac806fb822fe5477bd"

    #step 1 授权
    authorizeStr = client.authorize(appid=appid,code=code) #获得授权
    authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
    #获取用户资金余额
    access_url = "http://gw.open.ppdai.com/balance/balanceService/QueryBalance"
    access_token = "your_access_token"
    data = {}
    sort_data = rsa.sort(data)
    sign = rsa.sign(sort_data)
    list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)

```

```php
    authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
    echo authorizeResult;
    url = "http://gw.open.ppdai.com/balance/balanceService/QueryBalance";
    accessToken="yourAccessToken";
    request = '{}';
    result = send(url, request,accessToken);
    echo result
```

```shell
    curl http://gw.open.ppdai.com/fund/{open_id} \
    -d sign=xxx1
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
X-PPD-ACCESSTOKEN|	String	|是|	授权令牌|	8cf65377538741c2ba8add2615a22299


### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Results	|Int	|	|0
ResultMessage|	String	|处理信息	|返回文本信息
Balance|	Json	|账户科目分类及科目金额

> 返回值示例:

```json
[
    {
      "Result": 0,
      "ResultMessage": "",
      "Balance": [
        {
          "AccountCategory": "用户备付金.用户投标锁定",
          "Balance": 100
        },
        {
          "AccountCategory": "用户备付金.用户现金余额",
          "Balance": 0
        },
        {
          "AccountCategory": "用户备付金.用户提现锁定",
          "Balance": 0
        }
      ]
    }
]
```

### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-1	|系统异常信息	|稍后重试或联系客服
> 异常示例:

```json
[
    {
      "Result": -1,
      "ResultMessage": "系统异常信息",
      "Balance": null
    }
]
```

<aside class="notice">需要授权</aside>