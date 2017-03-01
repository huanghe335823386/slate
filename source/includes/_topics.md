# 专题(Topics)

## 认证规范(Authentication)

在调用 API 时，必须提供 API Key 作为每个请求的身份验证。你可以在管理平台内管理你的 API Key。API Key 是商户在 PPDAI 系统中的身份标识，请安全存储，确保其不要被泄露。如需获取或更新 API Key ，也可以在管理平台的「企业设置」->「开发设置」内进行操作。

PPDAI API 使用 HTTP Basic Auth 进行认证。 将 API Key 作为 basic auth 的用户名。不需要填写密码。

API Key 分为 live 和 test 两种模式。分别对应真实交易环境和模拟测试交易环境并且可以实时切换。测试模式下的 API Key 会模拟交易等请求，但是不会产生任何真实交易行为和费用，便于调试和接入。 所有的 API 请求必须通过 HTTPS 发送，使用 HTTP 会被 PPDAI 服务器拒绝。

## 错误规范(Error Code1)

PPDAI API 使用 HTTP 状态码 (status code) 来表明一个 API 请求的成功或失败状态。返回 HTTP 2XX 表明 API 请求成功。返回 HTTP 4XX 表明在请求 API 时提供了错误信息，例如参数缺失、参数错误、支付渠道错误等。返回 HTTP 5XX 表明 API 请求时，PPDai 服务器发生了错误。

__错误汇总__

返回属性 | 
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong


## 可扩展对象(Expand Object)

PPDAI 内有很多对象包含了其他对象的 id，如果这些对象带有 expandable 展开特性，你可以在请求参数后加入额外的展开参数来展开子对象。例如在创建 charge 对象时，使用 expand[]=app 参数来展开返回 charge 对象内部的 app 对象。


## 幂等请求(Idempotent Requests)


API必须支持幂等防止同一个请求意外提交执行两次。 例如， 当一个创建支付的请求因为网络连接错误失败时， 你可以使用一个幂等的key重新提交请求来保证只有一笔支付被创建。 

执行一个幂等请求，只需要在API的POST请求头部header中加上Idempotency-Key: <key>。 

如果生成唯一key由开发者决定。 我们建议使用随机字符串或者UUID。 
平台对所有包括相同的key的请求返回相同的请求。 
你不能在不同的请求参数中使用相同的key。 
key的有效期是24小时。 


## 元数据(Metadata)

一些 PPDai 对象支持加入用户指定的 metadata 参数。你可以使用键值对的形式来构建自己的 metadata，例如 metadata[color] = red，你可以在每一个 charge 对象中加入订单的一些详情，如颜色、型号等属性，在查询时获得更多信息。每一个对象的 metadata 最多可以拥有 10 个键值对，数据总长度在 1000 个 Unicode 字符以内。

## 分页控制(Paging)

所有的 PPDAI 资源都可以被 list API 方法支持，例如分页 charges 和 refunds。这些 list API 方法拥有相同的数据结构。PPDAI 是基于 cursor 的分页机制，使用参数 starting_after 来决定列表从何处开始，使用参数 ending_before 来决定列表从何处结束。


## 请求标识(Request IDs)

## 版本管理(Versions)