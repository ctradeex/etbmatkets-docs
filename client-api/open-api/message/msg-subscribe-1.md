# Msg Subscribe

## 环境地址&#x20;

> wss://pre-api-test.cmfbl.com/openapi-c /openMsg/{appId}

## 请求报文

> 发送心跳消息\
> `{"head":{"msgType":"ping","token":"fd5e62aa-1b7b-44bd-b693-43ef7a60e684app","sendTime":1628899424051,"lang":"zh-CN"},"device":1,"seqId":1434,"trace":"d141023c-c706-43f4-bfaf-e73132b1da52-1628899424051"}`
>
> \
> 发送登录消息\
> `{"head":{"msgType":"login","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"},"device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`
>
> \
> 发送订阅资产\
> `{"head":{"msgType":"subscribe_asset","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"}, "data":{"tradeTypes":"1"}, "device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`\
> \
> 发送取消订阅资产\
> `{"head":{"msgType":"cancel_subscribe_asset","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"}, "data":{"tradeTypes":"1"}, "device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`
>
> \
> 退出登录\
> `{"head":{"msgType":"logout","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"},"device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`

## **字段描述**

<table><thead><tr><th width="245">字段名称</th><th align="center">类型</th><th align="right">描述</th></tr></thead><tbody><tr><td>msgType</td><td align="center">String</td><td align="right">消息类型</td></tr><tr><td>sendTime</td><td align="center">Long</td><td align="right">发送时间</td></tr><tr><td>lang</td><td align="center">String</td><td align="right">语言</td></tr><tr><td>device</td><td align="center">String</td><td align="right">订阅设备类型</td></tr><tr><td>trace</td><td align="center">String</td><td align="right">跟踪号</td></tr><tr><td>tradeTypes</td><td align="center">String</td><td align="right">交易模式 1：合约全仓，2：合约逐仓，5：现货，6：股票</td></tr><tr><td>subscribeType</td><td align="center">String</td><td align="right">股票模式订阅类型（只有股票玩法需要传）1:仓位浮动盈亏，2:资产消息，仓位和资产一起同时订阅传1,2</td></tr><tr><td>companyId</td><td align="center">Long</td><td align="right">公司id</td></tr><tr><td>accountId</td><td align="center">Long</td><td align="right">账户id</td></tr><tr><td>customerId</td><td align="center">Long</td><td align="right">客户id</td></tr></tbody></table>



## **响应报文**

| 字段名称      |   描述   |
| --------- | :----: |
| msgCode   | 消息CODE |
| timestamp |  发送时间戳 |
| trace     |  追踪唯一码 |
| seqId     | 发送序列id |
| content   |  消息内容  |

