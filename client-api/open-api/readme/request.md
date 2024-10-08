---
description: Request
---

# Request

## 1. Request Address

{baseUrl}/openapi-c/global/{bizType}

| Parameter | Type   | Description                                                     |
| --------- | ------ | --------------------------------------------------------------- |
| baseUrl   | String | Request domain or IP, contact operational staff for details     |
| bizType   | String | Resource information. See the specific interface documentation. |

The DEMO is as follows:

POST https://prewppc-3.cmfbl.com/openapi-c/global/{bizType}

## 2. Request Method

Request Method: POST

## 3. Request Header Information

| Parameter  | Type   | Required | Description                                                   |
| ---------- | ------ | -------- | ------------------------------------------------------------- |
| companyId  | long   | Yes      | Unique company identifier                                     |
| trace      | String | Yes      | Unique identifier for global tracing                          |
| timestamp  | long   | Yes      | Request sending time, timestamp in milliseconds               |
| apiKey     | String | Yes      | API key applied through the platform                          |
| signature  | String | Yes      | Signature, see signature rules                                |
| recvWindow | long   | No       | Time window                                                   |
| version    | String | No       | Resource version number, see specific interface documentation |
| group      | String | No       | Resource group, see specific interface documentation          |
| lang       | String | No       | Language info, default is zh-CN                               |

## 4. Request Body Parameters

To be transmitted in the format content-type=application/json

Refer to specific interface documentation.

## 5. Response Format

Responses use JSON format.

All responses follow a unified format:

```json
{
  "code": "code",
  "message":"message",
  "data": null
}

```

## 6. Response Error Codes

| Code     | Description                               |
| -------- | ----------------------------------------- |
| 00012001 | Signature verification failed             |
| 00012002 | Request has exceeded the time window      |
| 00012003 | The requested API\_KEY does not exist     |
| 00012004 | No permission for the current API request |
| 00012005 | Request too frequent                      |
| 00012006 | API has expired                           |
| 00012007 | Illegal IP address                        |

## 7. Access Restrictions

* Currently, a single API-KEY can be accessed no more than 100 times per minute; otherwise, it will return 429.
* If requests continue after receiving a 429 response, it will return 418.
* The first time a 418 response is returned, the API key will be disabled for 5 minutes. Subsequent access attempts will increase the disable period to 10 minutes, and so on.
