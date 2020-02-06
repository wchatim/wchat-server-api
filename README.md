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


  

### Merchant Platform API

##### 1.转账
请求方法：`/mch/transfer`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| CT-Signature | String | 是 | CT-Nonce CT-Timestamp 拼接后hexSHA1加密，header参数传递 |
| reciver | String | 是 | 收款者openid |
| info | String | 是 | 转账信息 |
| quantity | String | 是 | 转账金额 |
| action | String | 是 | 转账动作：转账  提现  退币 |
| cid | String | 是 | 币种id |

----

##### 2.预下单
请求方法：`/mch/pay/order`

请求方式：`POST`

请求参数：
---
| 参数 | 类型 | 是否必填 | 参数说明 |
|:-------------:|:-------------|:-------------|:-------------|
| CT-Signature | String | 是 | CT-Nonce CT-Timestamp 拼接后hexSHA1加密，header参数传递 |
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

##### 3.商户余额查询
请求方法：`/mch/balance`

请求方式：`POST`

请求参数： 暂时未用到，待补充



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


