# wchat-server-api

### Development Platform API

##### 1.获取 access_token
请求方法：`/oauth/access_token`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| code | String | 是 | 授权登录获取的code |
| state | String | 是 | 授权登录获取的state |
| appid | String | 是 | appid |
| appsecret | String | 是 | 加密串 |
| grant_type | String | 是 | 填写：authorization_code |

----

响应结果：
```
{
    "msg": "Success",
    "data": {
        "access_token": "09cce11d21c1b08318b216d693be725d",
        "expires_in": 259200,
        "refresh_token": "a89e3c3db5214cc1a2472aa843c09c1a",
        "openid": "cfa0ac2506c442d9bf93cad95f695344",
        "scope": "*"
    },
    "code": "0"
}
```

##### 2.刷新 access_token
请求方法：`/oauth/refresh_token`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| appid | String | 是 | appid |
| refresh_token | String | 是 | 接口1返回参数 |
| grant_type | String | 是 | 填写：refresh_token |
----
响应结果：
```
{
    "msg": "Success",
    "data": {
        "access_token": "09cce11d21c1b08318b216d693be725d",
        "expires_in": 259200,
        "refresh_token": "a89e3c3db5214cc1a2472aa843c09c1a",
        "openid": "cfa0ac2506c442d9bf93cad95f695344",
        "scope": "*"
    },
    "code": "0"
}
```
##### 3.请求用户信息
请求方法：`/openapi/userinfo`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| access_token | String | 是 | 用户access_token |
| openid | String | 是 | 用户openid |

----
响应结果：
```
{
    "msg": "Success",
    "data": {
        "openid": "cfa0ac2506c442d9bf93cad95f695344",
        "nickname": "Apollo",
        "photo": "https://img.wchat.im/header/4128c3bdd4f941fe9f1ca0d5587ca967.jpg",
        "sex": "0",
        "grade": "0",
        "inviteCode": "758440"
    },
    "code": "0"
}
```

##### 4.获取邀请信息
请求方法：`/openapi/bindinfo`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| appid | String | 是 | appid |
| access_token | String | 是 | 用户access_token |
| openid | String | 是 | 用户openid |

----
响应结果：
```
{
    "msg": "Success",
    "data": {
        "openid": "a8d9af26d52d4190aab06e129879130e" //邀请人openid
    },
    "code": "0"
}
```

##### 5.获取用户币种余额
请求方法：`/openapi/balance`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| cid | String | 是 | 币种id |
| access_token | String | 是 | 用户access_token |
| openid | String | 是 | 用户openid |

响应结果：
```
{
    "msg": "Success",
    "data": {
        "cid": 20,
        "name": "EOS",
        "code": "EOS",
        "img": "https://wsr.oss-ap-southeast-1.aliyuncs.com/coins/ceos.png",
        "precision": 4,
        "contract": "eosio.token",
        "quantity": 0,
        "freeze": 0,
        "usdprice": "4.6619",
        "rmbprice": "32.6333"
    },
    "code": "0"
}
```

  

### Merchant Platform API

##### 1.转账
请求方法：`/mch/transfer`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| CT-Appid | String | 是 | 商户appid,header参数传递 |
| CT-Timestamp | String | 是 | 时间戳，header参数传递 |
| CT-Nonce | String | 是 | 随机数字串，header参数传递 |
| CT-Signature | String | 是 | 加密串，header参数传递，参考下边加密方式 |
| reciver | String | 是 | 收款者openid |
| info | String | 是 | 转账信息 |
| quantity | String | 是 | 转账金额 |
| action | String | 是 | 转账动作：转账  提现  退币 |
| cid | String | 是 | 币种id |

----

CT-Signature 签名方式：

```hexSHA1(商户加密串+CT-Nonce+CT-Timestamp)```

响应结果
```
{"msg":"Success","data":"b_f5afd80f3ec44b15ab4ec860a43cc903","code":"0"}
```

##### 2.预下单
请求方法：`/mch/pay/order`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| CT-Appid | String | 是 | 商户appid,header参数传递 |
| CT-Timestamp | String | 是 | 时间戳，header参数传递 |
| CT-Nonce | String | 是 | 随机数字串，header参数传递 |
| CT-Signature | String | 是 | 加密串，header参数传递，参考下边加密方式 |
| out_order_id | String | 是 | 订单id |
| notify_url | String | 是 | 支付后端回调地址 |
| openid | String | 是 | 下单用户openid |
| cid | String | 是 | 币种id |
| amount | String | 是 | 支付金额 |
| info | String | 是 | 支付信息 |
| action | String | 是 | 支付动作：pay |
| attach | String | 是 | 附加信息 |
| trade_type | String | 是 | 支付类型：CAPP |
| ip | String | 是 | 支付终端ip |

CT-Signature 签名方式：

```hexSHA1(商户加密串+CT-Nonce+CT-Timestamp)```

响应结果：
```
{
    "msg":"Success",
    "data":{
        "appid":"10233425",
        "mchid":"10244444",
        "nonce_str":"288d79fbf89b4e1eb5d47996117b1d21Dw2WcxH0",
        "sign":"70f4d2fad7f19bdcfedb6eb86b457dc0750baef9",
        "trade_type":"CAPP",
        "prepay_id":"21725138311446528"
    },
    "code":"0"
}
```

得到预下单返回结果，服务端重新生成返回参数：
`timestamp（自主生成）` `nonce(自主生成)` `orderid（预下单返回的prepay_id）` `paySign（预下单返回的sign）` 返回客户付支付

##### 3.下单回调
请求方法：`客户服务端的回调地址`

请求方式：`POST`

请求参数： 

| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| nonceStr | String | 是 | 随机串 |
| signature | String | 是 | 签名串 |
| out_order_id | String | 是 | 订单id |
| status | String | 是 | 状态，不等于"0"为成功 |

signature需要验签，验签方式

```String 本地签名串 = hexSHA1(商户id+商户加密串+nonceStr(回调参数))```

与回调参数signature比较，相同则验签正确，后边判断状态，进行业务处理



##### 4.商户余额查询
请求方法：`/mch/balance`

请求方式：`POST`

请求参数：
 
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| CT-Appid | String | 是 | 商户appid,header参数传递 |
| CT-Timestamp | String | 是 | 时间戳，header参数传递 |
| CT-Nonce | String | 是 | 随机数字串，header参数传递 |
| CT-Signature | String | 是 | 加密串，header参数传递，参考下边加密方式 |
| cid | String | 是 | 币种id |

CT-Signature 签名方式：

```hexSHA1(商户加密串+CT-Nonce+CT-Timestamp)```

响应结果：
```
{
    "msg":"Success",
    "data":{
        "cid":55,
        "name":"USDT",
        "code":"USDT",
        "img":"https://img.chattle.vip/coins/usdt.png",
        "precision":6,
        "contract":"0xdAC17F958D2ee523a2206206994597C13D831ec7",
        "quantity":0.337697,
        "freeze":0,
        "usdprice":"1",
        "rmbprice":"7"
    },
    "code":"0"
}
```


###  所有错误码
| 错误码 | 错误信息 |
|:-------------:|:-------------|
| 20015 | order push error |
| 20014 | order status error |
| 20013 | order status error |
| 20012 | order is expire |
| 20011 | order is finish |
| 20010 | merchant error |
| 20009 | orderid error |
| 20008 | amount error |
| 20007 | trade type error |
| 20006 | authorization error |
| 20005 | coin error |
| 20004 | reciver error |
| 20003 | signature error |
| 20002 | get open info error |
| 20001 | openid error |
| 10008 | refresh token error |
| 10007 | authorization code error |
| 10006 | app state error |
| 10005 | appserect error |
| 10004 | grant type error |
| 10003 | appid unavailable |
| 10002 | appid error |
| 10001 | respose type error |


