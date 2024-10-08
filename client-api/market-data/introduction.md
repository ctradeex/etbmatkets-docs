# Introduction

### Communication via websocket protocol <a href="#tong-guo-websocket-xie-yi-jin-xing-tong-xin" id="tong-guo-websocket-xie-yi-jin-xing-tong-xin"></a>

### Market Address Description <a href="#hang-qing-di-zhi-shuo-ming" id="hang-qing-di-zhi-shuo-ming"></a>

/quote Registered users in the Cryptocurrency Forex area

/quote\_guest Visitors to the Cryptocurrency Forex area

/quote\_stock Registered users in the stock area

Assume the provided url is wss://prewppc-3.cmfbl.com/apiQuote

If you want to register users in the digital currency foreign exchange area or the stock area, you need to add the token query string in the URL. No token is required to access the visitor market. Example:

wss://prewppc.trade.com/apiQuote/quote\_guest wss://prewppc.trade.com/apiQuote/quote?token=02d40878-3627-42bd-a61c-657fb4a3be55app wss://prewppc.trade.com/apiQuote/quote\_stock?token=02d40878-3627-42bd-a61c-657fb4a3be55app

### Introduction to Common Standard Request Headers <a href="#qing-qiu-tong-yong-biao-zhun-tou-jie-shao" id="qing-qiu-tong-yong-biao-zhun-tou-jie-shao"></a>

For the specific request message format, refer to the request examples in each interface.

| Fields  | name                    | type   | Required fields                                       | illustrate                                                                                                          |
| ------- | ----------------------- | ------ | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| cmd\_id | Protocol Number         | uint32 | See the individual interface definitions for details. |                                                                                                                     |
| seq\_id | Serial Number           | uint32 | yes                                                   | The requester generates a unique value, and the response will be consistent with the request                        |
| ext     | Tracking number (trace) | string | yes                                                   | The requester generates a unique field. The response will be consistent with the request. The maximum length is 64. |
| data    | Data body               | object | yes                                                   | For specific data formats, see the definitions of each interface.                                                   |

### Introduction to Common Standard Response Headers <a href="#ying-da-tong-yong-biao-zhun-tou-jie-shao" id="ying-da-tong-yong-biao-zhun-tou-jie-shao"></a>

For the specific response message format, refer to the response examples in each interface.

| Fields  | name                    | type   | illustrate                                                                                                          |
| ------- | ----------------------- | ------ | ------------------------------------------------------------------------------------------------------------------- |
| right   | Return Value            | int32  | Error code description                                                                                              |
| msg     | information             | string | A detailed description of success or failure                                                                        |
| cmd\_id | Protocol Number         | uint32 | See the individual interface definitions for details.                                                               |
| seq\_id | Serial Number           | uint32 | The requester generates a unique value, and the response will be consistent with the request                        |
| ext     | Tracking number (trace) | string | The requester generates a unique field. The response will be consistent with the request. The maximum length is 64. |
| data    | Data body               | object | For specific data formats, see the definitions of each interface.                                                   |
