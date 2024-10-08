# Request

## 1.Interface address=>HTTP

```
http://ip:port/path/
```

DEMO如下：

```http
POST http://127.0.0.1:9008/openapi-b/auth/{bizType} # auth
POST http://127.0.0.1:9008/openapi-b/{bizType} # request
...
```

Request method: POST

### 1.2 Request

```
Request header information
Request body information, transmitted in the form of content-type=application/json
```

#### 1.2.1 Header Request Parameters

| parameter | type   | required     | describe                                     |
| --------- | ------ | ------------ | -------------------------------------------- |
| companyId | long   | Required     | System unique company identifier             |
| trace     | String | Required     | Global link unique identifier                |
| timestamp | long   | Required     | Timestamp, milliseconds                      |
| version   | String | Not required | Interface version number                     |
| group     | String | Not required | Interface Grouping                           |
| lang      | String | Not required | Language information, default is zh-CN       |
| token     | String | Not required | Token information, required after logging in |

#### 1.2.2 Request Body Parameters

| parameter | type | required | describe                  |
| --------- | ---- | -------- | ------------------------- |
| bizBody   | JSON | Required | Request message body，JSON |

## 1.2 Interface address=>websocket

```
ws://ip:port/path/ws
```

The DEMO is as follows:

```
ws://127.0.0.1:9008/openapi-b/ws
```
