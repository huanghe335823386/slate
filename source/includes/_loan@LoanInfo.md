# 投标查询

##  投标列表接口 LoanList

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
        String url = "http://gw.open.ppdai.com/invest/LLoanInfoService/LoanList";
        Result result = OpenApiClient.send(url,
                new PropertyObject("PageIndex", 1, ValueTypeEnum.Int32),
                new PropertyObject("StartDateTime", "2015-11-11 12:00:00.000", ValueTypeEnum.DateTime));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```Net
            //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/LLoanInfoService/LoanList";
            Result Result = OpenApiClient.Send(Url,
                    new PropertyObject("PageIndex", 1, ValueTypeEnum.Int32),
                    new PropertyObject("StartDateTime", "2015-11-11 12:00:00.000", ValueTypeEnum.DateTime));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#新版投标列表接口（默认每页2000条）
access_url = "http://gw.open.ppdai.com/invest/LLoanInfoService/LoanList"
data = {
  "PageIndex": 1,
  "StartDateTime": "2015-11-11 12:00:00.000"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)
```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*新版投标列表接口（默认每页2000条）*/
$url = "http://gw.open.ppdai.com/invest/LLoanInfoService/LoanList";
$request = '{
  "PageIndex": 1,
  "StartDateTime": "2015-11-11 12:00:00.000"
}';
$result = send($url, $request);
echo $result

```

```Shell
curl http://gw.open.ppdai.com/invest/loans?limit={page_num} \
-d start_time="2015-11-11 12:00:00 000" \
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
PageIndex|	Int	|是	|页码|	1
StartDateTime	|DateTime|	否	|如果有则查询该时间之后的列表	|如果有则查询该时间之后的列表，精确到毫秒

> 请求参数示例:

```json
[
{
  "PageIndex": 1,
  "StartDateTime": "2015-11-11 12:00:00.000"
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int|	0：错误 1：成功 -1：异常|
ResultMessage|	String	|返回消息	|
ResultCode	|String|	暂未使用|
LoanInfos|	List	|列表信息	|
LoanInfos.ListingId	|Int	|列表ID	|
LoanInfos.Title|	String	|标的标题	|
LoanInfos.CreditCode|	String|	标的级别	|
LoanInfos.Amount	|Decimal	|借款金额	|
LoanInfos.Rate	|Double	|利率	|
LoanInfos.Months	|Int	|期限	|
LoanInfos.PayWay	|Int	|还款方式(0:等额本息(按月还款) 1:一次性还本付息)|
> 返回值示例:

```json
[
{
  "LoanInfos": [
    {
      "ListingId": 23886150,
      "Title": "手机app用户的借款",
      "CreditCode": "A",
      "Amount": 1000,
      "Rate": 12,
      "Months": 12,
      "PayWay": 0
    }
  ],
  "Result": 1,
  "ResultMessage": "查询成功",
  "ResultCode": null
}
]
```

## 散标详情批量接口 BatchListingInfos

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
        String url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingInfos";
        Result result = OpenApiClient.send(url,
                new PropertyObject("ListingIds", 1, ValueTypeEnum.Int32));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```Net
            //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingInfos";
            Result Result = OpenApiClient.Send(Url,
                    new PropertyObject("ListingIds", 1, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#新版散标详情批量接口（请求列表不大于10）
access_url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingInfos"
data = {
  "ListingIds": [
    23886149,
    23886150
  ]
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*新版散标详情批量接口（请求列表不大于10）*/
$url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingInfos";
$request = '{
  "ListingIds": [
    23886149,
    23886150
  ]
}';
$result = send($url, $request);
echo $result

```

```Shell
curl http://gw.open.ppdai.com/invest/loanitems \
-d listing_ids=[23886149,23886150] \
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
ListingIds	|List|	是	|列表IDs|
> 请求参数示例:

```json
[
{
  "ListingIds": [
    23886149,
    23886150
  ]
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int	|0：错误 1：成功 -1：异常	|
ResultMessage	|String|	返回消息	|
LoanInfos	|List|	列表信息	|
LoanInfos.FistBidTime	|DateTime	|首次投资时间	|
LoanInfos.LastBidTime	|DateTime|	末笔投资时间	|
LoanInfos.LenderCount	|Int	|投标人数	|
LoanInfos.AuditingTime	|DateTime|	成交日期	|
LoanInfos.RemainFunding	|Decimal|	剩余可投金额	|
LoanInfos.DeadLNetimeOrRemindTimeStr	|String	截止时间	|2016/11/19或者14天15时57分(剩余时间)
LoanInfos.CreditCode	|String|	标的等级|
LoanInfos.ListingId|	Int|	列表编号	|
LoanInfos.Amount	|Decimal	|借款金额|
LoanInfos.Months	|Int	|期限	|
LoanInfos.CurrentRate	|Double	|利率|
LoanInfos.BorrowName	|String	|借款人的用户名	|
LoanInfos.Gender	|Int|	性别	|1 男 2 女 0 未知	|
LoanInfos.EducationDegree	|String	|学历	|
LoanInfos.GraduateSchool	|String	|毕业院校	|
LoanInfos.StudyStyle	|String	|学习形式	|
LoanInfos.Age	|Int	|年龄	|
LoanInfos.SuccessCount	|Int	|成功借款次数	|
LoanInfos.WasteCount	|Int	|流标次数	|
LoanInfos.CancelCount	|Int	|撤标次数	|
LoanInfos.FailedCount	|Int	|失败次数	|
LoanInfos.NormalCount	|Int	|正常还清次数	|
LoanInfos.OverdueLessCount	|Int	|逾期(1-15)还清次数	|
LoanInfos.OverdueMoreCount	|Int	|逾期(15天以上)还清次数	|
LoanInfos.OwingPrincipal	|Decimal|	剩余待还本金	|
LoanInfos.OwingAmount	|Decimal	|待还金额	|
LoanInfos.AmountToReceive	|Decimal	|待收金额	|
LoanInfos.FirstSuccessBorrowTime	|DateTime	|第一次成功借款时间|
LoanInfos.RegisterTime	|DateTime|	注册时间	|
LoanInfos.CertificateValidate	|Int	|学历认证	0 未认证 1已认证	|
LoanInfos.NciicIdentityCheck	|Int	|户籍认证	0 未认证 1已认证	|
LoanInfos.PhoneValidate	|Int	|手机认证	0 未认证 1已认证	|
LoanInfos.VideoValidate	|Int	|视屏认证	0 未认证 1已认证	|
LoanInfos.CreditValidate	|Int|	征信认证	0 未认证 1已认证	|
LoanInfos.EducateValidate	|Int|	学籍认证	0 未认证 1已认证|
ResultCode	|String	|暂未使用|
> 返回值示例:

```json
[
{
  "LoanInfos": [
    {
      "FistBidTime": null,
      "LastBidTime": null,
      "LenderCount": 0,
      "AuditingTime": null,
      "RemainFunding": 1500,
      "DeadLineTimeOrRemindTimeStr": "2016/11/19",
      "CreditCode": "AA",
      "ListingId": 23886149,
      "Amount": 1500,
      "Months": 42,
      "CurrentRate": 12.0085,
      "BorrowName": "zhangsan",
      "Gender": 1,
      "EducationDegree": "专科",
      "GraduateSchool": "四川工业科技学院",
      "StudyStyle": "普通",
      "Age": 22,
      "SuccessCount": 0,
      "WasteCount": 0,
      "CancelCount": 0,
      "FailedCount": 0,
      "NormalCount": 0,
      "OverdueLessCount": 0,
      "OverdueMoreCount": 0,
      "OwingPrincipal": 0,
      "OwingAmount": 0,
      "AmountToReceive": 0,
      "FirstSuccessBorrowTime": null,
      "RegisterTime": "2016-11-04T04:57:40.473",
      "CertificateValidate": 1,
      "NciicIdentityCheck": 0,
      "PhoneValidate": 1,
      "VideoValidate": 0,
      "CreditValidate": 0,
      "EducateValidate": 1
    },
    {
      "xx": "……"
    }
  ],
  "Result": 1,
  "ResultMessage": "",
  "ResultCode": null
}
]
```


## 债转列表接口 DebtList

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
        String url = "http://gw.open.ppdai.com/invest/LLoanInfoService/DebtList";
        Result result = OpenApiClient.send(url,
                new PropertyObject("PageIndex", 1, ValueTypeEnum.Int32));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```Net
            //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/LLoanInfoService/DebtList";
            Result Result = OpenApiClient.Send(Url,
                    new PropertyObject("PageIndex", 1, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#新版债转列表接口（默认每页2000条）
access_url = "http://gw.open.ppdai.com/invest/LLoanInfoService/DebtList"
data = {
  "PageIndex": 1
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*新版债转列表接口（默认每页2000条）*/
$url = "http://gw.open.ppdai.com/invest/LLoanInfoService/DebtList";
$request = '{
  "PageIndex": 1
}';
$result = send($url, $request);
echo $result

```

```Shell
curl http://gw.open.ppdai.com/invest/debts?limit={page_num} \
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
PageIndex	|Int|	是	|页码	|
StartDateTime|	DateTime	|否	|如果有则查询该时间之后的列表，精确到毫秒|
> 请求参数示例:

```json
[
{
  "PageIndex": 1
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int|	0：错误 1：成功 -1：异常	|
ResultMessage|	String	|返回消息	|
ResultCode	|String|	暂未使用	|
DebtInfos	|List|	债转列表信息	|
DebtInfos.DebtdealId	|Int|	债权ID	|
DebtInfos.OwingNumber|	Int	|剩余期数	|
DebtInfos.PriceforSaleRate|	Decimal|	转让收益率	|
DebtInfos.PriceforSale	|Decimal|	转让价	|
DebtInfos.ListingId	|Int|	列表ID	||
DebtInfos.CreditCode	|String	|列表等级|
> 返回值示例:

```json
[
{
  "DebtInfos": [
    {
      "DebtdealId": 3314,
      "OwingNumber": 9,
      "PriceforSaleRate": 14,
      "PriceforSale": 37.95,
      "ListingId": 199878,
      "CreditCode": "B"
    }
  ],
  "Result": 1,
  "ResultMessage": "",
  "ResultCode": null
}
]
```


## 债转详情批量接口 BatchDebtInfos

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
        String url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchDebtInfos";
        Result result = OpenApiClient.send(url,
                new PropertyObject("DebtIds", 1, ValueTypeEnum.Int32));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```Net
            //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchDebtInfos";
            Result Result = OpenApiClient.Send(Url,
                    new PropertyObject("DebtIds", 1, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#新版债转详情批量接口（请求列表不大于20）
access_url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchDebtInfos"
data = {
  "DebtIds": [
    2594108
  ]
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*新版债转详情批量接口（请求列表不大于20）*/
$url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchDebtInfos";
$request = '{
  "DebtIds": [
    2594108
  ]
}';
$result = send($url, $request);
echo $result

```

```Shell
curl http://gw.open.ppdai.com/invest/debtitems \
-d debt_ids=[2594108,2594109] \
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
DebtIds|	List|	是	|债转列表IDs|

> 请求参数示例:

```json
[
    {
      "DebtIds": [
        2594108
      ]
    }
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int	|0：错误 1：成功 -1：异常	|
ResultMessage	|String	|返回消息	|
ResultCode	|String|	暂未使用|
DebtInfos	|List|	债转列表信息	|
DebtInfos.DebtId	|Int	|债转编号|
DebtInfos.Seller	|String|	转出人	|
DebtInfos.StatusId	|Int|	1出售中2已完成 0其它无效状态	|
DebtInfos.Lender|	String	|投标人	|
DebtInfos.BidDateTime	|DateTime	|投标时间	|
DebtInfos.OwingNumber	|Int|	剩余期数	|
DebtInfos.OwingPrincipal|	Decimal	|待还本金	|
DebtInfos.OwingInterest|	Decimal|	待收利息	|
DebtInfos.Days	|Int|	距离下次还款的天数	|
DebtInfos.PriceforSaleRate	|Decimal|	转让价利率	|
DebtInfos.PriceforSale	|Decimal|	转让价	|
DebtInfos.PreferenceDegree	|Decimal|	优惠度	|
DebtInfos.ListingId|	Int	|列表ID 原标的信息	|
DebtInfos.CreditCode|	String|	列表等级	|
DebtInfos.ListingAmount	|Decimal|	发标金额	|
DebtInfos.ListingMonths|	Int	|标期限	|
DebtInfos.ListingTime	|DateTime	|发标时间	|
DebtInfos.ListingRate	|Double	|标的利率	|
DebtInfos.PastDueNumber	|Int|	曾逾期期数|
> 返回值示例:

```json
[
{
  "DebtInfos": [
    {
      "DebtId": 2594108,
      "Seller": "zhangsan",
      "StatusId": 1,
      "Lender": "zhangsan",
      "BidDateTime": "2016-09-24T11:22:35.533",
      "OwingNumber": 11,
      "OwingPrincipal": 275.8,
      "OwingInterest": 9.75,
      "Days": -5,
      "PriceforSaleRate": 7.06,
      "PriceforSale": 276.16,
      "PreferenceDegree": 0,
      "ListingId": 20658281,
      "CreditCode": "AAA",
      "ListingAmount": 5000,
      "ListingTime": "2016-09-24T07:41:02.733",
      "ListingMonths": 12,
      "ListingRate": 7.01,
      "PastDueNumber": 0
    }
  ],
  "Result": 1,
  "ResultMessage": "",
  "ResultCode": null
}
]
```



## 列表投标详情批量接口 BatchListingBidInfos

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
        String url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingBidInfos";
        Result result = OpenApiClient.send(url,
                new PropertyObject("ListingIds", 1, ValueTypeEnum.Int32));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```Net
            //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingBidInfos";
            Result Result = OpenApiClient.Send(Url,
                    new PropertyObject("ListingIds", 1, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#新版列表投标详情批量接口（请求列表大小不大于5）
access_url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingBidInfos"
data = {
  "ListingIds": [
    100001
  ]
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*新版列表投标详情批量接口（请求列表大小不大于5）*/
$url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingBidInfos";
$request = '{
  "ListingIds": [
    100001
  ]
}';
$result = send($url, $request);
echo $result

```

```Shell
curl http://gw.open.ppdai.com/invest/bidlistingitems \
-d listing_ids=[100001,100002] \
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
ListingIds	|List	|是|	列表IDs|
> 请求参数示例:

```json
[
{
  "ListingIds": [
    100001
  ]
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int	|0：错误 1：成功 -1：异常	|
ResultMessage	|String	|返回消息	|
ResultCode	|String	|暂未使用	|
ListingBidsInfos	|List	|投标信息	|
ListingBidsInfos.ListingBidsInfo.ListingId	|Int	|列表ID	|
ListingBidsInfos.ListingBidsInfo.Bids	|List	|投标详情	|
ListingBidsInfos.ListingBidsInfo.Bids.LenderName|	String|	投资人	|
ListingBidsInfos.ListingBidsInfo.Bids.BidAmount	|Decimal|	投标金额	|
ListingBidsInfos.ListingBidsInfo.Bids.BidDateTime|	DateTime	|投标时间|
> 返回值示例:

```json
[
{
  "ListingBidsInfos": [
    {
      "ListingId": 100001,
      "Bids": [
        {
          "LenderName": "test1",
          "BidAmount": 50,
          "BidDateTime": "2016-12-22T10:23:47.16"
        },
        {
          "LenderName": "test2",
          "BidAmount": 50,
          "BidDateTime": "2016-12-22T10:27:57.47"
        },
        {
          "LenderName": "test3",
          "BidAmount": 100,
          "BidDateTime": "2016-12-22T10:28:11.517"
        }
      ]
    }
  ],
  "Result": 1,
  "ResultMessage": "查询成功",
  "ResultCode": null
}
]
```


## 列表状态查询批量接口 BatchListingStatusInfos

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
        String url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingStatusInfos";
        Result result = OpenApiClient.send(url,
                new PropertyObject("ListingIds", 1, ValueTypeEnum.Int32));
        System.out.println(String.format("返回结果:%s", result.isSucess() ? result.getContext() : result.getErrorMessage()));

```

```Net
            //应用id
            string Appid = "yourAppid";
            //私钥
            string ClientPrivateKey = "yourPrivateKey";
            //公钥
            string ServerPublicKey = "yourPublicKey";

            OpenApiClient.Init(Appid, PKCSType.PKCS8, ServerPublicKey, ClientPrivateKey);
            //请求Url
            String Url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingStatusInfos";
            Result Result = OpenApiClient.Send(Url,
                    new PropertyObject("ListingIds", 1, ValueTypeEnum.Int32));
            Console.WriteLine(Result);
```

```Python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#新版列表状态查询批量接口（请求列表大小不大于20条）
access_url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingStatusInfos"
data ={
  "ListingIds": [
    100000
  ]
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign)

```

```PHP
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*新版列表状态查询批量接口（请求列表大小不大于20条）*/
$url = "http://gw.open.ppdai.com/invest/LLoanInfoService/BatchListingStatusInfos";
$request = '{
  "ListingIds": [
    100000
  ]
}';
$result = send($url, $request);
echo $result

```

```Shell
curl http://gw.open.ppdai.com/invest/listing/status \
-d listing_ids=[100000,100001] \
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
ListingIds|	List|	是	|列表IDs|

> 请求参数示例:

```json
[
{
  "ListingIds": [
    100000
  ]
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int|	0：错误 1：成功 -1：异常	|
ResultMessage|	String	|返回消息	|
ResultCode	|String|	暂未使用|
Infos	|List|	列表状态信息|
Infos.ListingId|	Int|	列表ID|
Infos.Status|	Int	|0 :流标 1:满标 2: 投标中 3 :借款成功（成功 || 成功已还清） 4: 审核失败 5 :撤标|
> 返回值示例:

```json
[
{
  "Infos": [
    {
      "ListingId": 100000,
      "Status": 3
    }
  ],
  "Result": 1,
  "ResultMessage": "查询成功",
  "ResultCode": null
}
]
```
