# Ticker

### Interface Description <a href="#jie-kou-shuo-ming" id="jie-kou-shuo-ming"></a>

The interface feature is that for each websocket connection, each time the request is sent, the backend will overwrite the previous subscription request by default. After the subscription is successful, data will be pushed.

### Request-Protocol Number: 14000 <a href="#qing-qiu-xie-yi-hao-14000" id="qing-qiu-xie-yi-hao-14000"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json" id="shu-ju-ge-shi-json"></a>

#### Data Structure <a href="#shu-ju-jie-gou" id="shu-ju-jie-gou"></a>

**data definition**

| Fields       | name         | type  | Required fields | illustrate                                              |
| ------------ | ------------ | ----- | --------------- | ------------------------------------------------------- |
| symbol\_list | Product List | array | yes             | See the symbol definition below for the specific format |

**Symbol definition**

| Fields      | name             | type   | Required fields | illustrate                                                                               |
| ----------- | ---------------- | ------ | --------------- | ---------------------------------------------------------------------------------------- |
| symbol\_id  | Product ID       | uint64 | yes             |                                                                                          |
| trade\_type | Transaction Type | uint32 | yes             | 1: Full position contract, 2: Isolated position contract, 3: Leverage, 5: Spot, 6: Stock |
| trade\_mode | Trading Model    | uint32 | yes             | 1:MM, 2:ButterflyMM, 3:Matchmaking, 4:Aggregation                                        |

#### Request Example <a href="#qing-qiu-shi-li" id="qing-qiu-shi-li"></a>

Copy

```
{
    "cmd_id":14000,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
        "symbol_list": [
            {
                "symbol_id": 112312,
                "trade_type": 1,
                "trade_mode": 1,
            }
        ],
    }
}
```

### Response-Protocol Number: 14001 <a href="#ying-da-xie-yi-hao-14001" id="ying-da-xie-yi-hao-14001"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json-1" id="shu-ju-ge-shi-json-1"></a>

#### Data Structure <a href="#shu-ju-jie-gou-1" id="shu-ju-jie-gou-1"></a>

**data definition**

| Fields     | name               | type  | illustrate                                            |
| ---------- | ------------------ | ----- | ----------------------------------------------------- |
| tick\_list | tick snapshot data | array | See the tick definition below for the specific format |

**Tick ​​definition**

| Fields                  | name                                                  | type   | illustrate                                                                                     |
| ----------------------- | ----------------------------------------------------- | ------ | ---------------------------------------------------------------------------------------------- |
| symbol\_id              | Product ID                                            | uint64 |                                                                                                |
| trade\_type             | Transaction Type                                      | uint32 | 1: Full position contract, 2: Isolated position contract, 3: Leverage, 5: Spot, 6: Stock       |
| trade\_mode             | Trading Model                                         | uint32 | 1:MM, 2:ButterflyMM, 3:Matchmaking, 4:Aggregation                                              |
| seq                     | Quotation number                                      | uint64 |                                                                                                |
| tick\_time              | Quote timestamp                                       | uint64 |                                                                                                |
| price\_digits           | Price decimal places                                  | uint32 |                                                                                                |
| price                   | Latest transaction price                              | string |                                                                                                |
| tick\_deep              | Depth Quote                                           | array  | This depth will only bring one level of quote information, see the tick\_deep definition below |
| open\_price             | The opening price of the latest day                   | string |                                                                                                |
| close\_price            | The closing price of the latest day                   | string |                                                                                                |
| high\_price             | The highest price of K in the last day                | string |                                                                                                |
| low\_price              | The lowest price of K in the last day                 | string |                                                                                                |
| yesterday\_close\_price | The most recent day's daily K closing price yesterday | string |                                                                                                |

**tick\_deep definition**

| Fields      | name                           | type   | illustrate |
| ----------- | ------------------------------ | ------ | ---------- |
| price\_bid  | Buy price, buy price           | string |            |
| price\_ask  | Selling price, selling price   | string |            |
| volume\_bid | Buy one volume, buy volume     | string |            |
| volume\_ask | Selling volume, selling volume | string |            |

#### Example Response <a href="#ying-da-shi-li" id="ying-da-shi-li"></a>

Copy

```
{
    "ret":200,
    "msg":"ok",
    "cmd_id":14001,
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
                "price": "651.12",
                "tick_deep": [
                    {
                        "price_bid": "9.12",
                        "price_ask": "147.12",
                        "volume_bid": "9.12",
                        "volume_ask": "147.12",
                    },
                ],
                "open_price": "651.12",
                "close_price": "623.12",
                "high_price": "674.12",
                "low_price": "619.12",
                "yesterday_close_price": "623.12",
            },
        ]
    }    
}
```

### Push data <a href="#tui-song-shu-ju" id="tui-song-shu-ju"></a>

#### illustrate <a href="#shuo-ming" id="shuo-ming"></a>

This quote push mainly includes transaction and one-level depth quotes. It is a comprehensive quote push. The data content is a string. Currently, one quote is pushed at a time. The backend service will push the data to the requester who sends a real-time quote subscription request.

#### Field Explanation <a href="#zi-duan-jie-shi" id="zi-duan-jie-shi"></a>

p(product ID, quote transaction type, transaction mode, quote sequence number, quote timestamp, current price, first tier bid price, first tier ask price, first tier bid volume, first tier ask volume); “p(symbol\_id,trade\_type,trade\_mode,seq,tick\_time,price,price\_bid1,price\_ask1,volume\_bid1,volume\_ask1);” trade\_type value meaning 1: full position contract, 2: single position contract, 3: leverage, 5: spot, 6: stock trade\_mode value meaning 1: MM, 2: butterfly MM, 3: matching, 4: aggregation

#### Push data example <a href="#tui-song-shu-ju-shi-li" id="tui-song-shu-ju-shi-li"></a>

p(1123,1,0,1232312,34545435345,6.23,6.23,6.24,123,234);
