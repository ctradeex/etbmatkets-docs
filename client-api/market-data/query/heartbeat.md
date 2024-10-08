# Heartbeat

### Interface Description <a href="#jie-kou-shuo-ming" id="jie-kou-shuo-ming"></a>

The requester is required to send a heartbeat request every 10 seconds. If no heartbeat request is received within 30 seconds, it will be considered a timeout and the requester's websocket connection will be disconnected.

### Request-Protocol Number: 14008 <a href="#qing-qiu-xie-yi-hao-14008" id="qing-qiu-xie-yi-hao-14008"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json" id="shu-ju-ge-shi-json"></a>

#### Data Structure <a href="#shu-ju-jie-gou" id="shu-ju-jie-gou"></a>

**data definition**

#### Request Example <a href="#qing-qiu-shi-li" id="qing-qiu-shi-li"></a>

Copy

```
{
    "cmd_id":14008,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
    }
}
```

### Response-Protocol Number: 14009 <a href="#ying-da-xie-yi-hao-14009" id="ying-da-xie-yi-hao-14009"></a>

#### Data format:json <a href="#shu-ju-ge-shi-json-1" id="shu-ju-ge-shi-json-1"></a>

#### Data Structure <a href="#shu-ju-jie-gou-1" id="shu-ju-jie-gou-1"></a>

**data definition**

#### Example Response <a href="#ying-da-shi-li" id="ying-da-shi-li"></a>

Copy

```
{
    "ret":200,
    "msg":"ok",
    "cmd_id":14009,
    "seq_id":123,
    "ext":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
    }
}
```

[\
](https://docs-cn.multimarkets.org/client-api/bao-jia-jie-kou/cha-xun-jie-kou)
