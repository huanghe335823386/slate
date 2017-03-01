# 注册相关（Register）

以下接口为用户注册相关接口

## 发送注册验证码(SendSMSRegisterCode)

参数 | 必填 | 描述
---- | ---- | -----
Mobile<br/><em>String</em>|是|需要注册的手机号|
DeviceFP<br/><em>String</em>|是|设备编号，对应设备的唯一标识|

```java
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

```.net
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