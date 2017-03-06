# 投标

## 投标接口 Bidding

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
        String url = "http://gw.open.ppdai.com/invest/BidService/Bidding";
        Result result = OpenApiClient.send(url, accessToken,
                new PropertyObject("ListingId", 9575229, ValueTypeEnum.Int32),
                new PropertyObject("Amount",150, ValueTypeEnum.Double));
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
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/BidService/Bidding";
            Result Result = OpenApiClient.Send(Url, AccessToken,
                    new PropertyObject("ListingId", 9575229, ValueTypeEnum.Int32),
                    new PropertyObject("Amount", 150, ValueTypeEnum.Double));
            Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#投标接口
access_url = "http://gw.open.ppdai.com/invest/BidService/Bidding"
access_token = "your_access_token"
data = {
  "ListingId": 9575229,
  "Amount": 150
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)


```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*投标接口*/
$url = "http://gw.open.ppdai.com/invest/BidService/Bidding";
$accessToken="yourAccessToken";
$request = '{
  "ListingId": 9575229,
  "Amount": 150
}';
$result = send($url, $request,$accessToken);
echo $result
```

```shell
curl http://gw.open.ppdai.com/invest/{access_token}/{listing_id}/bid \
-d amount=50 \
-d sign="xxx1" \
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|	String|	是	|拍拍贷分配给开发者的应用Id|	9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP|	String	|是	|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN|	String	|是	|使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION	|Double|	否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double|	否|	服务器版本号,最新版本号为1	|1
X-PPD-SIGN	|String|	是|	使用私钥对请求报文体进行签名|
X-PPD-ACCESSTOKEN|	String	|是	|授权令牌|	8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
ListingId|	Int	|是	|标编号	|9575229
Amount	|Int|	是	|投标金额|	150

> 请求参数示例:

```json
[
{
  "ListingId": 9575229,
  "Amount": 150
}
]
```

### Response Parameters

参数 | 类型 |  描述| 示例值
--------- | ------- |---------|-------
istingId|	Int|	标编号	|
Amount|	Int|	投标金额	|
ParticipationAmount|	Int|	实际投标金额	|
Result|	Int	|返回码 0=成功， -1=失败|	0
ResultMessage	|String	|失败的消息	|
> 返回值示例:

```json
[
{
  "Result": 0,
  "ResultMessage": "null",
  "ListingId": "1123123",
  "Amount": "150",
  "ParticipationAmount": "50"
}
]
```
### ERROR CODE DESCRIPTION
名称|	描述|	解决方案
--------- | ------- | -----------
-1	|未知异常|	重新请求接口或联系开放平台维护人员
1002|	用户信息不存在|	请重新让用户授权，或联系开放平台维护人员
1001|	用户编号异常	|联系开放平台维护人员
2001|	标的编号异常|	请重新输入正确列表编号
2002	|标的不存在|	请重新输入正确列表编号或尝试更换其他列表编号
3001	|单笔投标金额只能是50-10000的整数	|请重新输入投标金额
3002|	累计投标金额不能＞20000元	|请重新输入投标金额
3003|	累计投标金额不能＞标的金额的30%	|请重新输入投标金额
3004|	不能给自己投标	|请重新输入列表编号
3005|	已满标	|请重新输入列表编号
4001|	账户余额不足，请先充值	|请充值或更换投标账号



## 我的投标接口 BidList

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
        String url = "http://gw.open.ppdai.com/invest/BidService/BidList";
        Result result = OpenApiClient.send(url, accessToken,
                new PropertyObject("ListingId", 9575229, ValueTypeEnum.Int32),
                new PropertyObject("StartTime","2016-03-21", ValueTypeEnum.DateTime),
                new PropertyObject("EndTime","2016-03-21", ValueTypeEnum.DateTime),
                new PropertyObject("PageIndex",1, ValueTypeEnum.Int32),
                new PropertyObject("PageSize",20, ValueTypeEnum.Int32));
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
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/BidService/BidList";
            Result Result = OpenApiClient.Send(Url, AccessToken,
                    new PropertyObject("ListingId", 9575229, ValueTypeEnum.Int32),
                    new PropertyObject("StartTime", "2016-03-21", ValueTypeEnum.DateTime),
                    new PropertyObject("EndTime", "2016-03-21", ValueTypeEnum.DateTime),
                    new PropertyObject("PageIndex", 1, ValueTypeEnum.Int32),
                    new PropertyObject("PageSize", 20, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#我的投标接口
access_url = "http://gw.open.ppdai.com/invest/BidService/BidList"
access_token = "your_access_token"
data = {
  "ListingId": 9575229,
  "StartTime": "2016-03-21",
  "EndTime": "2016-03-21",
  "PageIndex": 1,
  "PageSize": 20
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)


```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*我的投标接口*/
$url = "http://gw.open.ppdai.com/invest/BidService/BidList";
$accessToken="yourAccessToken";
$request = '{
  "ListingId": 9575229,
  "StartTime": "2016-03-21",
  "EndTime": "2016-03-21",
  "PageIndex": 1,
  "PageSize": 20
}';
$result = send($url, $request,$accessToken);
echo $result
```

```shell
curl http://gw.open.ppdai.com/invest/{access_token}/bid/{listing_id} \
-d start_time="2016-03-21" \
-d end_time="2016-03-21" \
-d page_index=1 \
-d page_size=20 \
-d sign="xxx1"
```

### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID|	String|	是	|拍拍贷分配给开发者的应用Id	|9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String	|是	|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN|	String	|是|	使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION|	Double|	否	|签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION|	Double|	否	|服务器版本号,最新版本号为1	|1
X-PPD-SIGN	|String|	是|	使用私钥对请求报文体进行签名
X-PPD-ACCESSTOKEN	|String	|是	|授权令牌|	8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
ListingId|	Int	|否	|按照标的查询输入标的号，否则输入0|	9575229
StartTime|	String	|否	|开始时间	|2016-03-21
EndTime|	String	|否|	结束时间	|2016-03-21
PageIndex|	Int	|否|	页码	|1
PageSize|	Int	|否|	每页数	|20
> 请求参数示例:

```json
[
{
  "ListingId": 9575229,
  "StartTime": "2016-03-21",
  "EndTime": "2016-03-21",
  "PageIndex": 1,
  "PageSize": 20
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
BidList.ListingId|	Int	|标编号	|
BidList.Title|	String|	标题	|
BidList.Months|	Int|	期数|	12
BidList.Rate|	Double|	利率	|7
BidList.Amount	|Decimal|	标的金额	|
BidList.BidAmount|	Int	|投标金额	|
BidList|	List|	记录数	|
TotalPages|	Int|	总页数|
TotalRecord|	Int	|总记录数	|
Result	|Int	|返回码 0=成功， -1=失败|	0
ResultMessage|	String|	失败的消息|
> 返回值示例:

```json
[
{
  "Result": 0,
  "ResultMessage": "null",
  "TotalPages": "1",
  "TotalRecord": "20",
  "BidList": {
    "Title": "测试使用",
    "ListingId": "223423",
    "Months": "10",
    "Rate": "10",
    "Amount": "10000",
    "BidAmount": "80"
  }
}
]
```



## 债转购买接口 BuyDebt

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
        String url = "http://gw.open.ppdai.com/invest/BidService/BuyDebt";
        Result result = OpenApiClient.send(url, accessToken,
                new PropertyObject("debtDealId", 38458234, ValueTypeEnum.Int32));
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
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/BidService/BuyDebt";
            Result Result = OpenApiClient.Send(Url, AccessToken,
                    new PropertyObject("debtDealId", 38458234, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#债转购买接口
access_url = "http://gw.open.ppdai.com/invest/BidService/BuyDebt"
access_token = "your_access_token"
data = {
  "debtDealId": 38458234
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)

```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*债转购买接口*/
$url = "http://gw.open.ppdai.com/invest/BidService/BuyDebt";
$accessToken="yourAccessToken";
$request = '{
  "debtDealId": 38458234
}';
$result = send($url, $request,$accessToken);
echo $result
```

```shell
curl http://gw.open.ppdai.com/invest/{access_token}/{debtdeal_id}/debt \
-d sign="xxx1"
```
### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID	|String	|是	|拍拍贷分配给开发者的应用Id|	9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP	|String|	是|	UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN|	String|	是	|使用私钥对应用ID+时间戳进行签名|
X-PPD-SIGNVERSION	|Double|	否|	签名验证版本号,最新版本号为1|	1
X-PPD-SERVICEVERSION	|Double	|否	|服务器版本号,最新版本号为1|	1
X-PPD-SIGN	|String	|是	|使用私钥对请求报文体进行签名	|
X-PPD-ACCESSTOKEN|	String|	是	|授权令牌	|8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
debtDealId	|Int|	是	|债转编号	|3242342
> 请求参数示例:

```json
[
{
  "debtDealId": 38458234
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int	|返回码 0=成功， -1=失败|	0
ResultMessage	|String|	失败的消息	|
debtDealId|	Int	|债转编号|
> 返回值示例:

```json
[
{
  "Result": 0,
  "ResultMessage": "null",
  "debtDealId": "3242342"
}
]
```


## 用户最近投资标的信息 BatchLenderBidList

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
        String url = "http://gw.open.ppdai.com/invest/BidService/BatchLenderBidList";
        Result result = OpenApiClient.send(url, accessToken,
                new PropertyObject("LenderNames", 38458234, ValueTypeEnum.Int32));
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
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/BidService/BatchLenderBidList";
            Result Result = OpenApiClient.Send(Url, AccessToken,
                    new PropertyObject("LenderNames", 38458234, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#（跟投）用户最近投资标的信息（批量）
access_url = "http://gw.open.ppdai.com/invest/BidService/BatchLenderBidList"
access_token = "your_access_token"
data = {
  "LenderNames": [
    "fell_2015"
  ],
  "TopIndex": 10
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)

```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*（跟投）用户最近投资标的信息（批量）*/
$url = "http://gw.open.ppdai.com/invest/BidService/BatchLenderBidList";
$accessToken="yourAccessToken";
$request = '{
  "LenderNames": [
    "fell_2015"
  ],
  "TopIndex": 10
}';
$result = send($url, $request,$accessToken);
echo $result

```

```shell
curl http://gw.open.ppdai.com/invest/{access_token}/bid?limit={page_num} \
-d lender_names=["fell_2015",""fell_2016"] \
-d sign="xxx1"
```

### Header Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
X-PPD-APPID	|String	|是	|拍拍贷分配给开发者的应用Id|	9f6a4c76e03c441ea0d3b8ff238311a0
X-PPD-TIMESTAMP|	String|	是	|UTC时间戳	|yyyy-MM-dd HH:mm:ss
X-PPD-TIMESTAMP-SIGN|	String	|是|	使用私钥对应用ID+时间戳进行签名	|
X-PPD-SIGNVERSION	|Double	|否|	签名验证版本号,最新版本号为1	|1
X-PPD-SERVICEVERSION	|Double	|否|	服务器版本号,最新版本号为1	|1
X-PPD-SIGN|	String | 是	|使用私钥对请求报文体进行签名	|
X-PPD-ACCESSTOKEN	|String	|是|	授权令牌|	8cf65377538741c2ba8add2615a22299

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
LenderNames|	List|	是	|投资用户名列表，个数1至5	|[ "fell" ],
TopIndex|	int|	是|	记录条数，1至20条	|10
> 请求参数示例:

```json
[
{
  "LenderNames": [
    "fell_2015"
  ],
  "TopIndex": 10
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|int	|0 成功，-1失败
ResultMessage	|String	|错误消息
ResultCode|	String	|暂未使用
LendersBidsList	|List|	详情列表
LendersBidsList.LenderName	|String	|投资人姓名
LendersBidsList.Bids	|Object	|详情
LendersBidsList.Bids.ListingId|	int	|标号
LendersBidsList.Bids.Title	|String	|标题
LendersBidsList.Bids.BidDateTime|	DateTime|	投标时间
LendersBidsList.Bids.BidAmount	|Decimal|	投标金额
LendersBidsList.Bids.BorrowerName	|String	|借款人
LendersBidsList.Bids.CreditCode	|String	|标等级
LendersBidsList.Bids.Amount	|Decimal	|标金额
LendersBidsList.Bids.Months|	int	|期限
LendersBidsList.Bids.Rate	|double|	利率
LendersBidsList.Bids.NciicIdentityCheck|	int|	户口认证0=未认证，1=已认证
LendersBidsList.Bids.CertificateValidate|	int	|学历认证0=未认证，1=已认证
LendersBidsList.Bids.PhoneValidate	|int|	手机认证0=未认证，1=已认证
LendersBidsList.Bids.VideoValidate	|int|	视屏认证0=未认证，1=已认证
LendersBidsList.Bids.CreditValidate	|int|	征信认证0=未认证，1=已认证
LendersBidsList.Bids.StatusId|	int	|0=流标，1=成功（投标状态)

> 返回值示例:

```json
[
{
  "LendersBidsList": [
    {
      "LenderName": "fell",
      "Bids": [
        {
          "ListingId": 2629971,
          "Title": "教育培训",
          "BidDateTime": "2016-09-19T23:40:59.853",
          "BidAmount": 1000,
          "BorrowerName": "pdu02278615",
          "CreditCode": "AA",
          "Amount": 3000,
          "Months": 12,
          "Rate": 11,
          "NciicIdentityCheck": 0,
          "CertificateValidate": 0,
          "PhoneValidate": 1,
          "VideoValidate": 0,
          "CreditValidate": 0,
          "StatusId": 1
        }
      ]
    }
  ],
  "Result": 0,
  "ResultMessage": "查询成功",
  "ResultCode": null
}
]
```


