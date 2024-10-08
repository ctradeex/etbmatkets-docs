---
description: MarketQuoteMarket
---

# Market

### Interface Description <a href="#jie-kou-shuo-ming" id="jie-kou-shuo-ming"></a>

The interface feature is that for each websocket connection, each time the request is sent, the backend will overwrite the previous subscription request by default. After the subscription is successful, data will be pushed.

### Request-Protocol Number: 14010 <a href="#qing-qiu-xie-yi-hao-14010" id="qing-qiu-xie-yi-hao-14010"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json" id="shu-ju-ge-shi-json"></a>

#### Data Structure <a href="#shu-ju-jie-gou" id="shu-ju-jie-gou"></a>

**data definition**

| Fields       | name         | type  | Required fields | illustrate                                              |
| ------------ | ------------ | ----- | --------------- | ------------------------------------------------------- |
| symbol\_list | Product List | array | yes             | See the symbol definition below for the specific format |

**Symbol definition**

| Fields             | name                              | type   | Required fields | illustrate                                                                                                                                                                                                                                                                              |
| ------------------ | --------------------------------- | ------ | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbol\_id         | Product ID                        | uint64 | yes             |                                                                                                                                                                                                                                                                                         |
| trade\_type        | Transaction Type                  | uint32 | yes             | 1: Full position contract, 2: Isolated position contract, 3: Leverage, 5: Spot, 6: Stock                                                                                                                                                                                                |
| trade\_mode        | Trading Model                     | uint32 | yes             | 1:MM, 2:ButterflyMM, 3:Matchmaking, 4:Aggregation                                                                                                                                                                                                                                       |
| depth\_level       | Depth level                       | uint32 | no              | If there is no depth\_level field, the backend will only provide a quote for one level. The requested level is greater than the actual quote level. If there is no depth\_level field, the backend will provide a quote for as many levels as the actual quote level has.               |
| merge\_accuracy    | Merge precision                   | string | yes             | If the value is 10, it means the quotation will be combined according to the tenth digit; if it is 1, it means the quotation will be combined according to each decimal place; if it is 0.001, it means the quotation will be combined according to the third decimal place, and so on. |
| trade\_info\_count | Number of transaction information | uint32 | yes             | Indicates how many transaction quotes you want to receive in response to your subscription.                                                                                                                                                                                             |

#### Request Example <a href="#qing-qiu-shi-li" id="qing-qiu-shi-li"></a>

Copy

```
{
    "cmd_id":14010,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
        "symbol_list": [
            {
		"symbol_id": 112312,
		"trade_type": 1,
                "trade_mode": 0,
                "depth_level": 5,
                "merge_accuracy":"0.001",
                "trade_info_count": 5,
            },
	],
    }
}
```

### Response-Protocol Number: 14011 <a href="#ying-da-xie-yi-hao-14011" id="ying-da-xie-yi-hao-14011"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json-1" id="shu-ju-ge-shi-json-1"></a>

#### Data Structure <a href="#shu-ju-jie-gou-1" id="shu-ju-jie-gou-1"></a>

**data definition**

| Fields     | name               | type  | illustrate                                            |
| ---------- | ------------------ | ----- | ----------------------------------------------------- |
| tick\_list | tick snapshot data | array | See the tick definition below for the specific format |

**Tick ​​definition**

| Fields        | name                    | type   | illustrate                                                                                                                              |
| ------------- | ----------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| symbol\_id    | Product ID              | uint64 |                                                                                                                                         |
| trade\_type   | Transaction Type        | uint32 | 1: Full position contract, 2: Isolated position contract, 3: Leverage, 5: Spot, 6: Stock                                                |
| trade\_mode   | Trading Model           | uint32 | 1:MM, 2:ButterflyMM, 3:Matchmaking, 4:Aggregation                                                                                       |
| seq           | Quotation number        | uint64 |                                                                                                                                         |
| tick\_time    | Quote timestamp         | uint64 |                                                                                                                                         |
| price\_digits | Price decimal places    | uint32 |                                                                                                                                         |
| bid\_deep     | bid depth               | array  | See the definition of bid\_deep below. The number of depths will vary depending on the depth\_level and merge\_accuracy in the request. |
| ask\_deep     | askDepth                | array  | See the definition of ask\_deep below. The number of depths will vary depending on the depth\_level and merge\_accuracy in the request. |
| trade\_info   | Transaction information | array  | See trade\_info definition below                                                                                                        |

**bid\_deep definition**

| Fields      | name                       | type   | illustrate |
| ----------- | -------------------------- | ------ | ---------- |
| price\_bid  | Buy price, buy price       | string |            |
| volume\_bid | Buy one volume, buy volume | string |            |

**ask\_deep definition**

| Fields      | name                           | type   | illustrate |
| ----------- | ------------------------------ | ------ | ---------- |
| price\_ask  | Selling price, selling price   | string |            |
| volume\_ask | Selling volume, selling volume | string |            |

**trade\_info definition**

| Fields           | name                  | type   | illustrate                                  |
| ---------------- | --------------------- | ------ | ------------------------------------------- |
| price            | Sold Price            | string |                                             |
| volume           | Volume                | string |                                             |
| trade\_direction | Trading direction     | uint32 | 0 is the default value, 1 is BUY, 2 is SELL |
| trade\_time      | Transaction timestamp | uint64 | Unit: Seconds                               |

#### Example Response <a href="#ying-da-shi-li" id="ying-da-shi-li"></a>

Copy

```
{
    "ret":200,
    "msg":"ok",
    "cmd_id":14011,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
        "tick_list":[
            {
		"symbol_id": 123,
		"trade_type": 1,
                "trade_mode": 0,
		"seq": 1605509068000001,
		"tick_time": 1605509068,
                "price_digits": 2,
		"bid_deep": [
                    {
			"price_bid": "9.12",
                        "volume_bid": "9.12",
                    },
		],
                "ask_deep": [
                    {
			"price_ask": "147.12",
			"volume_ask": "147.12",
                    },
		],
                "trade_info": [
                    {
			"price": "651.12",
                        "volume": "100",
                        "trade_direction": 1,
                        "trade_time": 1605509068,
                    },
		]
            },
        ]
    }    
}
```

### Push data - real-time transaction quotation push <a href="#tui-song-shu-ju-shi-shi-cheng-jiao-bao-jia-tui-song" id="tui-song-shu-ju-shi-shi-cheng-jiao-bao-jia-tui-song"></a>

#### illustrate <a href="#shuo-ming" id="shuo-ming"></a>

The quotation push mainly reflects the transaction information. The push data content is a string. Currently, one quotation is pushed at a time. The backend service will push the data to the requester only after the requester sends a quotation subscription request.

#### Field Explanation <a href="#zi-duan-jie-shi" id="zi-duan-jie-shi"></a>

pt(product ID, quote transaction type, transaction mode, quote sequence number, quote timestamp, current price, transaction volume, transaction direction); "pt(symbol\_id,trade\_type,trade\_mode,seq,tick\_time,price,volume,trade\_direction);" trade\_type value meaning 1: full position contract, 2: single position contract, 3: leverage, 5: spot, 6: stock trade\_mode value meaning 1: MM, 2: butterfly MM, 3: matching, 4: aggregation

#### Push data example <a href="#tui-song-shu-ju-shi-li" id="tui-song-shu-ju-shi-li"></a>

"pt(1123,1,0,1232312,34545435345,6.23,1000,1);"

### Push data-market quote push <a href="#tui-song-shu-ju-pan-kou-bao-jia-tui-song" id="tui-song-shu-ju-pan-kou-bao-jia-tui-song"></a>

#### illustrate <a href="#shuo-ming-1" id="shuo-ming-1"></a>

The quote push mainly reflects the market information, and will merge the deep quotes according to the merge precision field in the subscription request. The push data content is a string, and currently one quote is pushed at a time. The backend service will push the data to the requester only after the requester sends a market transaction quote subscription request.

#### Field Explanation <a href="#zi-duan-jie-shi-1" id="zi-duan-jie-shi-1"></a>

pd(product ID, quotation transaction type, transaction mode, quotation sequence number, quotation timestamp);(1st tier bid price, 1st tier bid volume)(2nd tier bid price, 2nd tier bid volume);(1st tier ask price, 1st tier ask volume)(2nd tier ask price, 2nd tier ask volume); "pd(symbol\_id,trade\_type,trade\_mode,seq,tick\_time);(price\_bid1,volume\_bid1)(price\_bid2,volume\_bid2);(price\_ask1,volume\_ask1)(price\_ask2,volume\_ask2);" trade\_type value meaning 1: full position contract, 2: single position contract, 3: leverage, 5: spot, 6: stock trade\_mode value meaning 1: MM, 2: butterfly MM, 3: matching, 4: aggregation

#### Push data example <a href="#tui-song-shu-ju-shi-li-1" id="tui-song-shu-ju-shi-li-1"></a>

"pd(1123,1,0,1232312,34545435345);(6.23,123)(6.22,256);(6.24,111)(6.25,222);" "pd(1123,1,0,1232312,34545435345) ;(6.23,123)(6.22,256);(6.24,111)(6.25,222)(6.25,333);" "pd(1123,1,0,1232312,34545435345);;(6.24,111)( 6.25,222)(6.25,333);"
