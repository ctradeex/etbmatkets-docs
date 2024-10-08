# Cancel

### Interface Description <a href="#jie-kou-shuo-ming" id="jie-kou-shuo-ming"></a>

### Request-Protocol Number: 14006 <a href="#qing-qiu-xie-yi-hao-14006" id="qing-qiu-xie-yi-hao-14006"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json" id="shu-ju-ge-shi-json"></a>

#### Data Structure <a href="#shu-ju-jie-gou" id="shu-ju-jie-gou"></a>

**data definition**

| Fields       | name              | type   | Required fields | illustrate                                                                                                                                                        |
| ------------ | ----------------- | ------ | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cancel\_type | Cancellation Type | uint32 | yes             | 0: Clear all subscriptions, 1: Unsubscribe from real-time quote push, 2: Unsubscribe from market price quote push, 3: Unsubscribe from 24-hour rolling quote push |

#### Request Example <a href="#qing-qiu-shi-li" id="qing-qiu-shi-li"></a>

Copy

```
{
    "cmd_id":14006,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
        "cancel_type": 1,
    }
}
```

### Response-Protocol Number: 14007 <a href="#ying-da-xie-yi-hao-14007" id="ying-da-xie-yi-hao-14007"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json-1" id="shu-ju-ge-shi-json-1"></a>

#### Data Structure <a href="#shu-ju-jie-gou-1" id="shu-ju-jie-gou-1"></a>

**data definition**

#### Example Response <a href="#ying-da-shi-li" id="ying-da-shi-li"></a>

Copy

```
{
    "ret":200,
    "msg":"ok",
    "cmd_id":14007,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
    }
}
```
