# 产品类目(Categories)

在拍拍贷交易资金平台，将使用类目作为债权产品的分类， 同一个分类下的产品具有一些共同的特征。 

## 定义类目对象(design)

属性 | 描述
--------- | -----------
ID<br/><em>String</em> | 对象 id ，由 PPDAI 生成，28 位长度字符串。| 
type<br/><em>String</em> | 对象类型，默认是category| 
name<br/><em>String</em> | 类目名称| 
title<br/><em>String</em> | 类目标题| 
desc<br/><em>String</em> | 类目描述| 
metadata<br/><em>Hash</em> | 扩展数据| 


## 创建类目对象(create)

```ruby
require 'category'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.categories.get
```

```python
import category

api = kittn.authorize('meowmeowmeow')
api.categories.get()
```

```shell
curl "http://api.ppdai.com/api/categories"
  -H "Authorization: meowmeowmeow"
```

```javascript
const category = require('category');

let api = category.authorize('meowmeowmeow');
let categories = api.categories.get();
```

> 响应示例:

```json
{
  "action" : "get",
  "application" : "1cc8e4be-c597-11e6-b61c-e22e7ab8dc1b",
  "params" : {
    "ql" : [ " order by created desc" ]
  },
  "path" : "/categories",
  "uri" : "http://localhost:8080/ibm/trump/categories",
  "entities" : [ {
    "uuid" : "75a2c039-c5ed-11e6-b9fa-e22e7ab8dc1b",
    "type" : "category",
    "name" : "test",
    "created" : 1482153435289,
    "modified" : 1482153435289,
    "metadata" : {
      "path" : "/categories/75a2c039-c5ed-11e6-b9fa-e22e7ab8dc1b",
      "size" : 319
    }
  } ],
  "timestamp" : 1482153446499,
  "duration" : 76,
  "organization" : "ppdai",
  "applicationName" : "trump",
  "count" : 1
}
```

查询类目列表。 

### HTTP 请求

`POST http://api.ppdai.com/api/categories`

### 查询参数(Parameter)

参数 | 缺省 | 描述
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## 查询类目对象列表(list)

> 请求示例:


```ruby
require 'Category'

api = Category::APIClient.authorize!('meowmeowmeow')
api.categories.get
```

```python
import category

api = category.authorize('meowmeowmeow')
api.categories.get()
```

```shell
curl "http://api.ppdai.com/api/v1/categories"
  -H "Authorization: meowmeowmeow"
```

```javascript
const category = require('category');

let api = category.authorize('meowmeowmeow');
let categories = api.categories.get();
```

> 返回示例:

```json
{
  "action" : "get",
  "application" : "1cc8e4be-c597-11e6-b61c-e22e7ab8dc1b",
  "params" : {
    "ql" : [ " order by created desc" ]
  },
  "path" : "/categories",
  "uri" : "http://localhost:8080/ibm/trump/categories",
  "entities" : [ {
    "uuid" : "75a2c039-c5ed-11e6-b9fa-e22e7ab8dc1b",
    "type" : "category",
    "name" : "test",
    "created" : 1482153435289,
    "modified" : 1482153435289,
    "metadata" : {
      "path" : "/categories/75a2c039-c5ed-11e6-b9fa-e22e7ab8dc1b",
      "size" : 319
    }
  } ],
  "timestamp" : 1482153446499,
  "duration" : 76,
  "organization" : "ibm",
  "applicationName" : "trump",
  "count" : 1
}
```

你可以使用调用该接口来查询对应的 category 对象列表信息。

### HTTP 请求

`GET http://api.ppdai.com/api/categories`

### 查询参数(Parameter)

参数 | 缺省 | 描述
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.


### HTTP请求

`GET http://api.ppdai.com/api/categories`

### 查询参数(Parameter)


参数 | 默认 | 描述
--------- | ------- | -----------
limit |  | 返回数据的数目
ql |  | 查询语句


<aside class="success">
备注 — ql支持复杂条件查询!
</aside>


## 查询特定类目对象(get)

```ruby
require 'category'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.categories.get
```

```python
import category

api = kittn.authorize('meowmeowmeow')
api.categories.get()
```

```shell
curl "http://api.ppdai.com/api/categories"
  -H "Authorization: meowmeowmeow"
```

```javascript
const category = require('category');

let api = category.authorize('meowmeowmeow');
let categories = api.categories.get();
```

> 响应示例:

```json
{
  "action" : "get",
  "application" : "1cc8e4be-c597-11e6-b61c-e22e7ab8dc1b",
  "params" : {
    "ql" : [ " order by created desc" ]
  },
  "path" : "/categories",
  "uri" : "http://localhost:8080/ibm/trump/categories",
  "entities" : [ {
    "uuid" : "75a2c039-c5ed-11e6-b9fa-e22e7ab8dc1b",
    "type" : "category",
    "name" : "test",
    "created" : 1482153435289,
    "modified" : 1482153435289,
    "metadata" : {
      "path" : "/categories/75a2c039-c5ed-11e6-b9fa-e22e7ab8dc1b",
      "size" : 319
    }
  } ],
  "timestamp" : 1482153446499,
  "duration" : 76,
  "organization" : "ibm",
  "applicationName" : "trump",
  "count" : 1
}
```

查询类目列表。 

### HTTP 请求

`GET http://api.ppdai.com/api/categories`

### 查询参数(Parameter)

参数 | 缺省 | 描述
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>
