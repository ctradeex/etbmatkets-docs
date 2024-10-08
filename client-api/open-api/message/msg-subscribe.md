---
description: Msg Subscribe
---

# Msg Subscribe

## Environment Address

> wss://pre-api-test.cmfbl.com/openapi-c/openMsg/{appId}

## Request Messages

> Sending Heartbeat Message\
> `{"head":{"msgType":"ping","token":"fd5e62aa-1b7b-44bd-b693-43ef7a60e684app","sendTime":1628899424051,"lang":"zh-CN"},"device":1,"seqId":1434,"trace":"d141023c-c706-43f4-bfaf-e73132b1da52-1628899424051"}`

> Sending Login Message\
> `{"head":{"msgType":"login","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"},"device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`

> Sending Subscribe Asset\
> `{"head":{"msgType":"subscribe_asset","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"}, "data":{"tradeTypes":"1"}, "device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`

> Sending Cancel Subscribe Asset\
> `{"head":{"msgType":"cancel_subscribe_asset","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"}, "data":{"tradeTypes":"1"}, "device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`

> Sending Logout Message\
> `{"head":{"msgType":"logout","token":"74e6e8df-9399-4bec-85aa-217c9b93e38eapp","sendTime":1628899396299,"lang":"zh-CN"},"device":1,"seqId":1222,"trace":"12321229-c31b-4c52-8471-9f27fd61e9e8-1628899396299"}`

## Field Descriptions

| Field Name    |  Type  | Description                                                                                                                                                    |
| ------------- | :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| msgType       | String | Message type                                                                                                                                                   |
| sendTime      |  Long  | Sending time                                                                                                                                                   |
| lang          | String | Language                                                                                                                                                       |
| device        | String | Subscription device type                                                                                                                                       |
| trace         | String | Trace number                                                                                                                                                   |
| tradeTypes    | String | Mode types (1: Contract Full, 2: Contract Isolated, 6: Stock)                                                                                                  |
| subscribeType | String | Stock mode subscription type (only for stock mode) (1: Position floating profit and loss, 2: Asset message, for both position and asset subscription pass 1,2) |
| companyId     |  Long  | Company ID                                                                                                                                                     |
| accountId     |  Long  | Account ID                                                                                                                                                     |
| customerId    |  Long  | Customer ID                                                                                                                                                    |

## Response Messages

| Field Name | Description         |
| ---------- | ------------------- |
| msgCode    | Message CODE        |
| timestamp  | Sending timestamp   |
| trace      | Trace unique code   |
| seqId      | Sending sequence ID |
| content    | Message content     |
