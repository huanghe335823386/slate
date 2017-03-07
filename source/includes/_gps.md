# CPS (CPS)
提供发标接口

## 用户信息添加 UserInfoAdd

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
        String url = "http://gw.open.ppdai.com/cps/BdRegService/UserInfoAdd";
        Result result = OpenApiClient.send(url, accessToken,
                new PropertyObject("SourceId", 0, ValueTypeEnum.Int32),
                new PropertyObject("PlatformType", 2, ValueTypeEnum.Int32),
                new PropertyObject("Info", "{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房，目前无房贷','chechan':'有车，但是有车贷未还清','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水 10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}", ValueTypeEnum.String),
                new PropertyObject("OrderId", "5765465456423465", ValueTypeEnum.String));
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
            String Url = "http://gw.open.ppdai.com/cps/BdRegService/UserInfoAdd";
            Result Result = OpenApiClient.Send(Url, AccessToken,
                    new PropertyObject("SourceId", 0, ValueTypeEnum.Int32),
                    new PropertyObject("PlatformType", 2, ValueTypeEnum.Int32),
                    new PropertyObject("Info", "{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房，目前无房贷','chechan':'有车，但是有车贷未还清','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水 10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}", ValueTypeEnum.String),
                    new PropertyObject("OrderId", "5765465456423465", ValueTypeEnum.String));
            Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#用户信息添加
access_url = "http://gw.open.ppdai.com/cps/BdRegService/UserInfoAdd"
access_token = "your_access_token"
data = {
  "SourceId": 0,
  "PlatformType": 2,
  "Info": "{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房，目前无房贷','chechan':'有车，但是有车贷未还清','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水 10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}",
  "OrderId": "5765465456423465"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)

```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*用户信息添加*/
$url = "http://gw.open.ppdai.com/cps/BdRegService/UserInfoAdd";
$accessToken="yourAccessToken";
$request = '{

}';
$result = send($url, $request,$accessToken);
echo $result
```

```shell
curl http://gw.open.ppdai.com/cps/fill \
-d sourceid=0 \
-d platformtype=2 \
-d info=xx \
-d orderid=5765465456423465 \
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

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
PlatformType|	Int	|是	|平台类型1：PC; 2:移动	|2
Info|	String|	否	|用户额外的详细信息 （可选）JSON格式	|
OrderId	|String|	否	|订单号（可选） - 这个用户的唯一标志，例如：用户ID	|123456465465
SourceId|	Int|	否	|	0

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

### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result	|Int	|返回码 0=成功， 1=失败|	0
ResultCode|	String|	暂时没用到	|
ResultMessage|	string	|失败的消息	|
Content|String	|RedirectUrl 表示要跳转的地址 (需要Url解码一下)	|{"RedirectUrl":""}


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

<aside class="notice">需要授权</aside>


## 发标接口 RegAfterPostListing

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
        String url = "http://gw.open.ppdai.com/cps/postlistingservice/regafterpostlisting";
        Result result = OpenApiClient.send(url, accessToken,
                new PropertyObject("RealName", "张三", ValueTypeEnum.String),
                new PropertyObject("ShenFenZH", "XXXXXXXXXXXXXXXXXX", ValueTypeEnum.String),
                new PropertyObject("ApplyLoanMonth", 12, ValueTypeEnum.Int32),
                new PropertyObject("ApplyLoanAmount", 1000, ValueTypeEnum.Double),
                new PropertyObject("DaiKuanYT","用于购物", ValueTypeEnum.String),
                new PropertyObject("LoanType", "10", ValueTypeEnum.String),
                new PropertyObject("Info", "'{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房,目前无房贷','chechan':'有车,但是有车贷未还','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}'", ValueTypeEnum.String),
                new PropertyObject("OrderId", "123456789", ValueTypeEnum.String));
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
            String Url = "http://gw.open.ppdai.com/cps/postlistingservice/regafterpostlisting";
            Result Result = OpenApiClient.Send(Url, AccessToken,
                    new PropertyObject("RealName", "张三", ValueTypeEnum.String),
                    new PropertyObject("ShenFenZH", "XXXXXXXXXXXXXXXXXX", ValueTypeEnum.String),
                    new PropertyObject("ApplyLoanMonth", 12, ValueTypeEnum.Int32),
                    new PropertyObject("ApplyLoanAmount", 1000, ValueTypeEnum.Double),
                    new PropertyObject("DaiKuanYT", "用于购物", ValueTypeEnum.String),
                    new PropertyObject("LoanType", "10", ValueTypeEnum.String),
                    new PropertyObject("Info", "'{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房,目前无房贷','chechan':'有车,但是有车贷未还','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}'", ValueTypeEnum.String),
                    new PropertyObject("OrderId", "123456789", ValueTypeEnum.String));
            Console.WriteLine(Result);
```

```python
appid="a769b53eb26849eba5d5e81ccb381a32"

code = "5ae2ee0d135b47ac806fb822fe5477bd"

#step 1 授权
authorizeStr = client.authorize(appid=appid,code=code) #获得授权
authorizeObj = pickle.loads(authorizeStr) # 将返回的authorize对象反序列化成对象，成功得到 OpenID、AccessToken、RefreshToken、ExpiresIn
#发标接口
access_url = "http://gw.open.ppdai.com/cps/postlistingservice/regafterpostlisting"
access_token = "your_access_token"
data = {
  "RealName": "张三",
  "ShenFenZH": "XXXXXXXXXXXXXXXXXX",
  "ApplyLoanMonth": 12,
  "ApplyLoanAmount": 1000,
  "DaiKuanYT": "用于购物",
  "LoanType": "10",
  "Info": "'{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房,目前无房贷','chechan':'有车,但是有车贷未还','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}'",
  "OrderId": "123456789"
}
sort_data = rsa.sort(data)
sign = rsa.sign(sort_data)
list_result = client.send(access_url,json.dumps(data) , appid, sign,access_token)


```

```php
/*step 1 通过code获取授权信息*/
$authorizeResult = authorize("dbff240axxxx4a0e9501e0954a7cda4d");
echo $authorizeResult;
/*发标接口*/
$url = "http://gw.open.ppdai.com/cps/postlistingservice/regafterpostlisting";
$accessToken="yourAccessToken";
$request = '{
  "RealName": "张三",
  "ShenFenZH": "XXXXXXXXXXXXXXXXXX",
  "ApplyLoanMonth": 12,
  "ApplyLoanAmount": 1000,
  "DaiKuanYT": "用于购物",
  "LoanType": "10",
  "Info": "'{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房,目前无房贷','chechan':'有车,但是有车贷未还','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}'",
  "OrderId": "123456789"
}';
$result = send($url, $request,$accessToken);
echo $result
```

```shell
curl http://gw.open.ppdai.com/cps/{access_token}/borrow \
-d real_name=zhangsan \
-d shenfen_zh=310xxxxxxxxxxxxxxx \
-d loan_month=12 \
-d loan_amount=1000 \
-d purpose="用于购物" \
-d loan_type=10 \
-d info="{xx:1}" \
-d order_id=123456789 \
-d sign="xxx1" \
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

### Request Parameters

参数 | 类型 | 必填 | 描述| 示例值
--------- | ------- | -----------|---------|-------
RealName	|String|	是	|真实姓名|	张三
ShenFenZH	|String|	是	|身份证号|	340321XXXXXXXX0815
ApplyLoanMonth	|Int	|是	|申请贷款期限	|10
ApplyLoanAmount	|Decimal|	是	|申请贷款金额	|1000
DaiKuanYT	|String	|是	|贷款用途	|用于购物
LoanType	|String	|是	|贷款类型|	10
Info	|String	|是	|用户详细信息json	|
OrderId	|String	|否	|订单号 - 渠道推送记录时带的唯一标志	|123456789

> 请求参数示例:

```json
[
{
  "RealName": "张三",
  "ShenFenZH": "XXXXXXXXXXXXXXXXXX",
  "ApplyLoanMonth": 12,
  "ApplyLoanAmount": 1000,
  "DaiKuanYT": "用于购物",
  "LoanType": "10",
  "Info": "'{'name':'孙XX','shenfenzh':'3XXXXXXXXXXXXXXXX5','zhiye':'上班族','fangchan':'有房,目前无房贷','chechan':'有车,但是有车贷未还','phone':'157XXXXXXXX','gongzixingshi':'现金','jingyingzz':'有','yuexin':'1500~3000','shebao':'连续6个月以内','duigongliushui':'半年银行流水10万以下','fuzhaiqingkuang':'有','applyCity':'蚌埠','money':'3000','month':'12','daikuanlx':'个人贷款','chushengnian':'1996','xinyong':'少量逾期','gongsiliushui':'3万以下','jingyingzhucedi':'本地'}'",
  "OrderId": "123456789"
}
]
```
### Response Parameters
参数 | 类型 | 描述| 示例值
--------- |  -----------|---------|-------
Result|	Int|	-1异常,0错误,1成功,-100处理中（IBdRegService中的UserInfoAdd方法除外:0 成功，-1失败）	|
ResultMessage|	String	|返回消息	|
Content	|String	|预留信息|
> 返回值示例:

```json
[
{
  "Result": 1,
  "ResultMessage": "发标成功",
  "Content": { }
}
]
```
<aside class="notice">需要授权</aside>