# Historical K-line

### Interface Description <a href="#jie-kou-shuo-ming" id="jie-kou-shuo-ming"></a>

Note: The server performs libz compression on the entire packet.

### Request-Protocol Number: 14012 <a href="#qing-qiu-xie-yi-hao-14012" id="qing-qiu-xie-yi-hao-14012"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json" id="shu-ju-ge-shi-json"></a>

#### Data Structure <a href="#shu-ju-jie-gou" id="shu-ju-jie-gou"></a>

**data definition**

| Fields                | name                        | type   | Required fields | illustrate                                                                                                                                                                                                                                                                                                                                                                                                         |
| --------------------- | --------------------------- | ------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| symbol\_id            | Product ID                  | uint64 | yes             |                                                                                                                                                                                                                                                                                                                                                                                                                    |
| trade\_type           | Transaction Type            | uint32 | yes             | 1: Full position contract, 2: Isolated position contract, 3: Leverage, 5: Spot, 6: Stock                                                                                                                                                                                                                                                                                                                           |
| trade\_mode           | Trading Model               | uint32 | yes             | 1:MM, 2:ButterflyMM, 3:Matchmaking, 4:Aggregation                                                                                                                                                                                                                                                                                                                                                                  |
| kline\_type           | K-line type                 | uint32 | yes             | 1 minute K, 2 is 5 minute K, 3 is 15 minute K, 4 is 30 minute K, 5 is hour K, 6 is 2 hour K, 7 is 4 hour K, 8 is daily K, 9 is weekly K, 10 is monthly K                                                                                                                                                                                                                                                           |
| kline\_timestamp\_end | Line end timestamp          | uint64 | no              | Unit: Seconds                                                                                                                                                                                                                                                                                                                                                                                                      |
| query\_kline\_num     | Query the number of K lines | uint32 | yes             | kline\_timestamp\_end is 0, query\_kline\_num is not 0, query the latest query\_kline\_num K-lines (including the current K-line) kline\_timestamp\_end is not 0, query\_kline\_num is not 0, query the query\_kline\_num K-lines from kline\_timestamp\_end to the previous query\_kline\_num K-lines In other cases, the interface directly returns an error, indicating that the query service is not supported |

#### Request Example <a href="#qing-qiu-shi-li" id="qing-qiu-shi-li"></a>

Copy

```
{
    "cmd_id":14012,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
        "symbol_id": 1,
        "trade_type": 1,
        "trade_mode": 0,
        "kline_type": 1,
        "kline_timestamp_end": 1605509068,
        "query_kline_num": 100,
    }
}
```

### Response-Protocol Number: 14013 <a href="#ying-da-xie-yi-hao-14013" id="ying-da-xie-yi-hao-14013"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json-1" id="shu-ju-ge-shi-json-1"></a>

#### Data Structure <a href="#shu-ju-jie-gou-1" id="shu-ju-jie-gou-1"></a>

**data definition**

| Fields        | name                 | type   | illustrate                                                                                                                                               |
| ------------- | -------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| symbol\_id    | Product ID           | uint64 |                                                                                                                                                          |
| trade\_type   | Transaction Type     | uint32 | 1: Full position contract, 2: Isolated position contract, 3: Leverage, 5: Spot, 6: Stock                                                                 |
| trade\_mode   | Trading Model        | uint32 | 1:MM, 2:ButterflyMM, 3:Matchmaking, 4:Aggregation                                                                                                        |
| kline\_type   | K-line type          | uint32 | 1 minute K, 2 is 5 minute K, 3 is 15 minute K, 4 is 30 minute K, 5 is hour K, 6 is 2 hour K, 7 is 4 hour K, 8 is daily K, 9 is weekly K, 10 is monthly K |
| price\_digits | Price decimal places | uint32 |                                                                                                                                                          |
| kline\_list   | K-line list          | array  | See the kline\_list definition below for the specific format.                                                                                            |

**kline\_list definition**

| Fields               | name                                      | type   | illustrate         |
| -------------------- | ----------------------------------------- | ------ | ------------------ |
| timestamp            | The timestamp of the K line               | uint64 | Unit: Seconds      |
| open\_price          | The opening price of the K-line           | string |                    |
| close\_price         | The closing price of the K-line           | string |                    |
| high\_price          | The highest price of the K line           | string |                    |
| low\_price           | The lowest price of the K line            | string |                    |
| last\_tick\_time     | The last tick time of the K line          | uint64 | Unit: milliseconds |
| last\_tick\_seq      | The last tick number of the K-line        | uint64 |                    |
| transactions\_number | The number of transactions of this K line | string |                    |

#### Example Response <a href="#ying-da-shi-li" id="ying-da-shi-li"></a>

Copy

```
{
    "ret":200,
    "msg":"ok",
    "cmd_id":14013,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
        "symbol_id": 1123,
        "trade_type": 1,
        "trade_mode": 0,
        "kline_type": 1,
        "price_digits": 2,
        "kline_list":[
            {
                "timestamp": 1605509068,
                "open_price": "651.12",
                "close_price": "623.12",
                "high_price": "674.12",
                "low_price": "619.12",
                "last_tick_time": 1605509068000001,
                "last_tick_seq": 1605509068000001,
                "transactions_number": "12345.6",
            },
        ]
    }    
}
```

[\
](https://docs-cn.multimarkets.org/client-api/bao-jia-jie-kou/cha-xun-jie-kou/xin-tiao)
