# Order Process

## Subscription Trade Messages:

### 1.Obtain token

Call the API: [Get Token](https://docs.multimarkets.org/client-api/open-api/message/get-msg-token)

Extract the \`data\` field from the response; this is the token.

### 2.Subscribe to Trade Messages:

Refer to the API documentation: [Message Subscription](https://docs.multimarkets.org/client-api/open-api/message/msg-subscribe)

#### 2.1 Establish Connection

PRE environment address: wss://pre-api-test.cmfbl.com/openapi-c/openMsg/{appId}

#### 2.2 Send Login Message:

```
{"device":1,"head":{"lang":"en-US","msgType":"login","sendTime":1698299047686,"token":"dbe3d3e6-0b10-4bdc-9778-dfc76c6d9341app"},"seqId":3,"trace":"x-1698299047686-4"}  
```

#### 2.3 Send Subscription Message:

```
{"data":{"tradeTypes":"2"},"device":1,"head":{"lang":"en-US","msgType":"subscribe_asset","sendTime":1698299047686,"token":"dbe3d3e6-0b10-4bdc-9778-dfc76c6d9341app"},"seqId":5,"trace":"x-1698299047686-6"}  
```

#### 2.4 Send Heartbeat Message Every 15 Seconds to Maintain Connection:

```
{"device":1,"head":{"lang":"en-US","msgType":"ping","sendTime":1698299057667,"token":"dbe3d3e6-0b10-4bdc-9778-dfc76c6d9341app"},"seqId":7,"trace":"x-1698299057667-8"}
```

## Order Process:

### 1.Request Product Information:

Call the API: [Product Brief Data](https://docs.multimarkets.org/client-api/open-api/base/symbol-base-info)Extract symbolId and symbolDigits for later use.

### 2.Request Customer Information:

Call the API: [Query Customer Information](https://docs.multimarkets.org/client-api/open-api/customer/customer-info)Extract accountId, digits, and currency from the entry in accountList with trade\_type=2.

### 3.Place Order:

Call the API: [Place Order](https://docs.multimarkets.org/client-api/open-api/trade/contract-order)

Example：\
http header:

```
Version: 0.01  
Group: tradeApi  
Trace: [Custom unique string] 
Content-Type: application/json  
Accept: application/json  
Apikey: [Already provided.]  
Timestamp: [Millisecond timestamp]
CompanyId: [Already provided (Test field: 439)] 
Signature: Signature, the generation rules are here <https://mtf.readme.io/reference/sgin, with example reference.>
```

http body：

```
{
     "accountCurrency":"CNY", //Parameters obtained in step 2
     "accountDigits":2, //Parameters obtained in step 2
     "accountId":1034124, //Parameters obtained in step 2
     "bizType":1, //Currently only supports these four types: business types, 1-market price opening; 2-market price flat; 13-limit price opening order; 14-limit price closing order
     "crossLevelNum":1, //fixed with 1
     "direction":1, //Order buying and selling direction, 1-buy; 2-sell;
     "entryType":1, //Order type 1 by quantity, 2 by amount
     "expireType":1, //limit order expiration type, 1-valid on the day; 2-valid on the week;
     "requestNum":"0.100000", //Order lot size or order amount, used with entryType
     "requestPrice":"167655", //The decimal place obtained in step 1 is used to convert the quotation into an integer. For example, if the decimal place is 3 and the quotation is 1.23, it will be converted to: 1230
     "requestTime":1698299972000,
     "symbolId":8390, //Parameters obtained in step 1
     "tradeType":2 //Fixed to 2
}
```

### 4.Handle Response

Upon receiving a response from step 3, check if code is “0”. If it is, the order placement is successful. Extract the orderId field from the data and match it with the orderId in the trade message.

Trade Message Fields:

```
{
     "trace":"x-1698310473323-102_b_bb76b676-8d8e-4278-82be-6ae7e063c9d3",
     "msgCode":"trade", //Only need to pay attention to msgCode=trade
     "content":{
         "accountId":1034124,
         "companyId":439,
         "bizType":"POSITION_OPEN", //POSITION_OPEN: Market price opening was successful, POSITION_CLOSE: Market price closing was successful, ME_POSITION_LIMIT_OPEN: Limit price opening was successful, ME_POSITION_LIMIT_CLOSE: Limit price closing was successful POSITION_OPEN_FAIL: Market price opening failed, ME_POSITION_LIMIT_FAIL: Limit price opening was Warehouse failed
         "customerId":2482,
         "paramMap":{
             "date":"1698310474529",
             "orderType":"1",
             "symbolId":"8390",
             "dealExecuteTime":"1698310474529",
             "orderBizType":"1",
             "orderId":"21257491", //Order ID
             "pendingId":"0",
             "dealId":"21262382",
             "accountCurrency":"CNY",
             "orderStatus":"2", //Order status: 1-order received; 2-order completed; 3-order partially completed; 4-order canceled; 5-order partially canceled; 6-order rejected; 7-order expired ;
             "dealExecuteNum":"8000.0",
             "source":"H5",
             "dealPrice":"1.67094", //Transaction price
             "requestAmount":"0.08",
             "takeProfitMsg":"--",
             "currency":"CNY",
             "symbolName":"EURAUD",
             "contractSize":"100000", //Contract size
             "sourceExecuteVolSum":"0.100000",
             "commission":"0",
             "sourceExecuteVol":"0.100000",
             "direction":"2",
             "dealAmount":"0.08", //Number of lots traded
             "accountId":"1034124",
             "companyId":"439",
             "positionId":"2023102650229", //Position ID
             "dealExecutePrice":"1.67094",
             "playType":"2",
             "orderDirection":"2",
             "symbolDigits":"5",
             "stopLossMsg":"--",
             "Margin":"59371.20"
         },
         "tradeType":2
     },
     "timestamp":1698310474563
}
```
