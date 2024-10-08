---
description: >-
  Through the WS protocol, you can subscribe to the full amount of user
  transaction data
icon: server
---

# Data Push

## Url Address

wss://pre-api-test.cmfbl.com/openapi-b/ws

## Related enumerations

### Trading mode(tradeType)

Trading mode (tradeType), you can fill in 1, 2, 5;

1. Full-position contract mode
2. Single-position contract mode
3. Spot mode

{% hint style="info" %}
Note: Currently, only Full-position contract mode, Single-position contract mode, and Spot  trading modes are supported. Other modes are not supported yet.
{% endhint %}

### Order type (bizType)

Full-position contract (1):

1. MARKET\_OPEN(1, "Market open"),
2. MARKET\_CLOSE(2, "Market close"),
3. STOP\_LOSS(3, "Stop loss close"),
4. TAKE\_PROFIT(4, "Take profit close"),
5. STOP\_OUT(5, "Forced close"),
6. SETTLEMENT(6, "Expiration close"),
7. CLEAR\_ACCOUNT(7, "Account cancellation close"),
8. MANUAL\_FORCE\_CLOSE(8, "Manual forced close"),
9. LIMIT\_OPEN(12, "Limit open")

Single-position contract (2):

1. MARKET\_OPEN(1, "Market open"),
2. MARKET\_CLOSE(2, "Market close"),
3. STOP\_LOSS(3, "Stop loss close"),
4. TAKE\_PROFIT(4, "Take profit close"),
5. STOP\_OUT(5, "Forced close"),
6. SETTLEMENT(6, "Expiration close"),
7. CLEAR\_ACCOUNT(7, "Account cancellation close"),
8. MANUAL\_FORCE\_CLOSE(8, "Manual forced close"),
9. LIMIT\_OPEN(12, "Limit open")

Spot trading method (5):

1. MARKET(12, "Market price"),
2. LIMIT(13, "Limit price");

### Order status (orderStatus)

```
INITIAL(0), //Default initial value
PLACED(1), //Order received
FILLED(2), //Order fulfilled
PARTIAL_FILLED(3), //Order partially fulfilled
CANCELLED(4), //Order canceled
PARTIAL_CANCELLED(5), //Order partially canceled
REJECTED(6), //Order rejected
EXPIRED(7), //Order expired
PROCESSING(8), //In progress
FINISH(9), //Finished
REVOKE(10), //Revoked
INTERNAL_ERROR(11), //Third party succeeded, CATS system encountered an exception
FAILURE(12), //Failed
PARTIAL_FAILURE(13) //Partial failure
```



### Subject Type（subjectType）：

```
1 Margin balance
2 Margin frozen
3 Margin available
4 Liability balance
5 Liability frozen
6 Liability available
7 Recoverable frozen
8 Recoverable frozen-frozen
9 Recoverable frozen available
19 Occupied margin balance
20 Occupied margin frozen
21 Occupied margin available
22 Interest balance
23 Interest frozen
24 Interest available
25 Collateral balance
26 Collateral frozen
27 Collateral available
```



## Business data push

{% code overflow="wrap" %}
```
Interconnection process description:
1. Get token through the authentication interface;
2. Place the token in the heander and establish a websocket link with the server.
The key in the header is the token. In addition, the group field can also be specified in the header. If multiple connections are required, please do not repeat the value of the group field. When the group value is the same, they will be kicked out.
3. To ensure that data is not lost and can be retransmitted after the link is interrupted, you need to ensure that the subscribed group is unique
4. The new group will be pushed from the new time point
Example:
header={"token": "608e3f81-1e10-481e-a917-6d256571e561admin", "group": "cats"}

The address is as follows:
ws://pre-api-test.cmfbl.com/openapi-b/ws
3. Wait for the server to push data;
4. Send heartbeat data regularly, the content is a ping string, and return the pong binary message of the websocket pong protocol, and the heartbeat cycle is 10s;

Note: Event messages will be saved for 168 hours (one week), and the messages will be cleared when the deadline is exceeded. In addition, when a group subscription client you specify is temporarily offline, the event messages generated during this period will be pushed to you when it is online again.
```
{% endcode %}

### Customer account registration (register)

```json
{
"data": {// Event data object
"companyId": 1,// Company id
"country": "CN",// Country
"createTime": 1645167068853,// Creation time
"customerGroupId": 1,// Customer group id
"customerNo": "86000079",// Customer number
"ext2": "",// Three-party unique code information, original value
"ext4": "",// Three-party unique code information, decrypted value
"id": "80",// Customer id
"kycAuditRemark": "Company has not opened KYC certification, directly passed",// kyc audit result description
"kycAuditStatus": 2,// kyc audit status, 0 uncertified, 1 pending audit, 2 audit passed, 3 audit failed
"language": "zh-CN", // Language information
"optional": 0, // Optional flag 0 Not added 1 Added
"phone": "18451251563", // Phone number
"phoneArea": ​​"+86", // Phone area code
"email": "", // Email address
"emailArea": ​​"", // Email area code
"registerSource": 4, // Registration source, 1=Mobile web: H5, 2=pcweb: PC_Web, 3=System & backend liquidation: System, 4=Android native app: Android, 5=Apple native app: iOS, 6=Hongmeng OS: HOS, 7=pc windows client: PC_Win, 8=pc mac client: PC_Mac, 9=None of the above: Other
"registerType": 2, // Registration method, 1 Email, 2 Phone number, 3 Customer account
"status": // 1 Status: 1 Normal, 2 Disabled, 3 Deleted, 4 Cancelled, 5 Locked, 6 Cancelled
},
"eventType": "register"// Event type
}
```

### Customer information update (customer\_update)

```json
{
"data":{
"birthday":"", //Date of birth (kyc backfill)
"companyId":362, //Company ID
"country":"CN", //Country
"createBy":"admin", //Created by
"createTime":1640077504114, //Created time
"customerGroupId":1, //Customer group
"customerNo":"86000000", //Customer account
"email":"123@163.com", //Email
"emailArea":"+86", //Email area code
"firstOpenAccountTime":1640077504157, //First account opening time
"id":"1", //ID
"kycAuditRemark":"Company has not opened KYC certification, directly passed", //KYC audit notes
"kycAuditStatus":2, //Registration KYC audit status: 1 pending audit, 2 audit passed, 3 audit failed (KYC backfill)
"language":"zh-CN", //language information
"loginIp":"210.22.23.4", //login ip
"loginTime":1640242095732, //login time
"optional":1, //optional flag 0 not added 1 added
"phone":"15920358625", //mobile phone
"phoneArea":"+86", //mobile phone area code
"revision":0, //version information
"status":1, //status: 1 normal, 2 disabled, 3 deleted, 4 account cancellation, 5 locked, 6 account cancellation in progress
"updateBy":"admin", //update person
"updateTime":1640242095735 //update time
},
"eventType":"customer_update"
}
```

### Add customer details (customer\_info\_insert)

```json
{
"data": {
"companyId": 439, // Company ID
"unitId": 13, // Unit ID
"country": "HK", // Country code
"registerIp": "1.1.1.1", // Registered IP
"registerDevice": "XX", // Registered device model
"utmSource": "xxx", // Advertising source (Account opening link parameter: source)
"utmMedium": "xxx", // Advertising medium (Account opening link parameter: medium)
"utmCampaign": "xxx", // Advertising campaign (Account opening link parameter: campaign)
"utmContent": "xxx", // Advertising content (Account opening link parameter: content)
"utmTerm": "xxx", // Keyword (Account opening link parameter: term)
"province": "", // Province
"city": "", // City
"address": "", // Detailed address
"remark": "xx", // Remarks
"ext1": "", // Extension field 1
"ext2": "", // Extension field 2
"ext3": "", // Extension field 3
"ext4": "", // Extension field 4
"ext5": "", // Extension field 5
"createBy": "86002812", // Creator
"createTime": 1704263677778, // Creation time
"customerInfoId": 2813, // Customer information ID
"customerNo": "86002812", // Customer number
"id": "2813", // Customer information ID
"revision": 0, // Version information
"status": 1 // Status (1: Enable, 2: Disable, 3: Delete)
},
"eventType": "customer_info_insert" // Event type
}
```

### Customer details update (customer\_info\_update)

```json
{
"data": {
"companyId": 439, // Company ID
"unitId": 13, // Unit ID
"country": "HK", // Country code
"registerIp": "1.1.1.1", // Registered IP
"registerDevice": "XX", // Registered device model
"utmSource": "xxx", // Advertising source (account opening link parameter: source)
"utmMedium": "xxx", // Advertising medium (account opening link parameter: medium)
"utmCampaign": "xxx", // Advertising campaign (account opening link parameter: campaign)
"utmContent": "xxx", // Advertising content (account opening link parameter: content)
"utmTerm": "xxx", // Keyword (account opening link parameter: term)
"province": "", // Province
"city": "", // City
"address": "", // Detailed address
"remark": "xx", // Remarks
"ext1": "", // Extension field 1
"ext2": "", // Extension field 2
"ext3": "", // Extension field 3
"ext4": "", // Extension field 4
"ext5": "", // Extension field 5
"createBy": "86002812", // Creator
"createTime": 1704263677778, // Creation time
"updateBy": "86002812", // Updater
"updateTime": 1704263677778, // Update time
"customerInfoId": 2813, // User detailed information ID
"customerNo": "86002812", // User number
"id": "2813", // User detailed information ID
"revision": 0, // Version information
"status": 1 // Status (1: Enable, 2: Disable, 3: Delete)
},
"eventType": "customer_info_update" // Event type
}

```

### kyc level certification passed (kyc)

```json
{
"data": {
"approval": "admin",//Approver
"approvalTime": 1647310823650,//Approval timestamp
"businessCode": "1",//Business code. The specific business interface application values are, open_account, cashin, withdraw, [My] - [Identity Authentication] applications are all 1
"companyId": 2, // Company id
"createTime": 1647310815202, // Creation timestamp
"customerNo": "86000018", // Customer number
"ext1": "KYC_WEB_ADD", // Extension field 1
"ext2": "19", // Extension field 2
"id": "20", // Record id
"levelCode": "level_2", // kyc level
"pathCode": "AF", // kyc path
"pno": "K556059077701009408", // kyc proposal number
"revision": 0, // Data version
"status": 2, // Status, 1 pending review, 2 approved, 3 unapproved
"updateBy": "admin", // Updater
"updateTime": 1647310823650//Update time
},
"eventType": "kyc"
}
```

### Open a trading account (open\_account)

```json
{
"data": {
"activateStatus": 1,//Activation status (1-unavailable, 2-available)
"companyId": 1,//Company id
"createTime": 1645167254541,//Creation time
"currency": 1,//Account opening asset id
"currencyCode": "USDT",//Account opening currency
"customerId": 81,//Customer id
"customerNo": "86000080",//Customer number
"digits": 6,//Decimal places of funds
"id": "1001394",//Account ID
"status": 2,// Account status (1-unavailable, 2-available)
"tradeType": 5, // Gameplay ID
"type": 1, // Account category (1-user, 2-merchant, 3-platform)
"updateTime": 1645167254541 // Update time
},
"eventType": "open_account"
}
```

### Account information update (account\_update)

```json
{
"data": {
"activateStatus": 1, // Activation status (1-unavailable, 2-available)
"companyId": 1, // Company id
"createTime": 1645167254541, // Creation time
"currency": 1, // Account opening asset id
"currencyCode": "USDT", // Account opening currency
"customerId": 81, // Customer id
"customerNo": "86000080", // Customer number
"digits": 6, // Decimal digits of funds
"id": "1001394", // Account ID
"status": 2, // Account status (1-unavailable, 2-available)
"tradeType": 5, // Gameplay ID
"type": 1, // Account category (1-user, 2-merchant, 3-platform)
"updateTime": 1645167254541//Update time
},
"eventType": "account_update"
}
```

### Account subject update (subject\_insert)

Subscription type is 1, which is to obtain account balance

```
{
"data": {
"accountId": 1000083, // Account id
"amount": 0, // Amount
"createTime": 1658738398243,//Creation time
"digits": 6,//Decimal places of amount
"id": "601",//Primary key of id
"type": 7,//Account type (1-balance, 2-freeze, 3-available, 4-liability balance, 5-liability frozen, 6-liability available, 7-freeze available, 8-freeze available-free, 9-freeze available, 10-platform balance, 11-platform frozen, 12-platform available, 13-institutional fund balance, 14-institutional fund frozen, 15-institutional fund available, 16-payable withdrawal balance, 17-payable withdrawal fund frozen, 18-payable withdrawal available, 19-occupied margin balance, 20-occupied margin frozen, 21-occupied margin available, 22-interest balance, 23-interest frozen, 24-interest available, 25-collateral balance, 26-collateral frozen, 27-collateral available)
"updateTime": 1658738398244,//Update time
"version": 0// Version number
},
"eventType": "subject_insert"
}
```

### Account subject update (subject\_update)

Subscription type is 1, which is to obtain account balance

```
{
"data": {
"accountId": 1000083,// Account id
"amount": 0,// Amount
"createTime": 1658738398243,// Creation time
"digits": 6,// Amount decimal places
"id": "601",// ID primary key
"type": 7,// Account type (1-balance, 2-freeze, 3-available, 4-liability balance, 5-liability frozen, 6-liability available, 7-freeze available, 8-freeze available-freeze, 9-freeze available, 10-platform balance, 11-platform frozen, 12-platform available, 13-institutional fund balance, 14-institutional fund frozen, 15-institutional fund available, 16-payable withdrawal balance, 17-payable withdrawal fund frozen, 18-payable withdrawal available, 19-occupied margin balance, 20-occupied margin frozen, 21-occupied margin available, 22-interest balance, 23-interest frozen, 24-interest available, 25-collateral balance, 26-collateral frozen, 27-collateral available)
"updateTime": 1658738398244, //Update time
"version": 0 //Version number
},
"eventType": "subject_update"
}
```

### Added account change details (subject\_water\_insert)

```json
{
"data": {
"accountId": 1000087,//Account id
"accountType": 1,//Account type
"amountAfter": 11210000000,//Amount after update
"amountIn": 11210000000,//Account deposit amount
"amountOut": 11210000000,//Account withdrawal amount
"bookkeepId": 2022072500115,//Voucher record id
"businessType": 603,// Business type (Full-position contract type [1-Deposit, 2-Withdrawal, 3-System clearing, 4-Quota adjustment, 5-Freeze, 6-Trading, 36-Transfer, 42-Reward]; Single-position contract type: [7-Deposit, 8-Withdrawal, 9-System clearing, 10-Quota adjustment, 11-Freeze, 12-Trading, 13-Adjust margin, 37-Transfer, 43-Reward]; Leverage type: [14-Deposit, 15-Withdrawal, 16-Quota adjustment, 17-Freeze, 18-Trading, 19-Automatic borrowing, 20-Manual borrowing, 21-Automatic repayment, 22-Manual repayment, 23-Loan interest interest, 35-background repayment, 38-transfer, 40-forced liquidation repayment, 44-reward]; spot leverage matching: [50-deposit, 51-withdrawal, 52-quota adjustment, 53-freeze, 54-trading, 55-transfer, 59-reward]; stock [601-deposit, 602-withdrawal, 603-quota adjustment, 604-freeze, 605-collateral, 606-trading, 607-loan, 608-repayment, 609-transfer, 610-interest calculation, 611-interest settlement, 612-reward, 613-system clearing, 614-company action])
"businessType1": 60301,// Sub-business type (Full-position contract type [1001-Front-end deposit, 1002-Deposit fee, 2001-Front-end withdrawal, 2002-Cancel withdrawal, 2003-Withdrawal fee, 2004-Cancel fee, 2005-Confirm transfer, 3001-System clear, 4001-Quota adjustment deposit, 4002-Quota adjustment withdrawal, 4003-Quota adjustment other, 4004-Quota adjustment bonus, 4005-Quota adjustment release cannot be withdrawn, 4006-Quota adjustment release cannot be withdrawn, 4007-Quota adjustment release cannot be withdrawn, 4008-Quota adjustment release cannot be withdrawn, 4009-Quota adjustment release cannot be withdrawn, 4010-Quota adjustment release cannot be withdrawn, 4011-Quota adjustment release cannot be withdrawn, 4012-Quota adjustment release cannot be withdrawn, 4013-Quota adjustment release cannot be withdrawn, 4014-Quota adjustment release cannot be withdrawn, 4015-Quota adjustment release cannot be withdrawn, 4016-Quota adjustment release cannot be withdrawn, 4017-Quota adjustment release cannot be withdrawn, 4018-Quota adjustment release cannot be withdrawn, 4019-Quota adjustment release cannot be withdrawn, 4020-Quota adjustment release cannot be withdrawn, 4021-Quota adjustment release cannot be withdrawn, 4022-Quota adjustment release cannot be withdrawn, 4023-Quota adjustment release cannot be withdrawn, 4024-Quota adjustment release cannot be withdrawn, 4025-Quota adjustment release cannot be withdrawn, 4026-Quota adjustment release cannot be withdrawn, 4027-Quota adjustment release cannot be -Quota adjustment cannot be withdrawn, 4007-Quota adjustment transferred to rebate, 5001-Freeze, 5002-Unfreeze, 6001-Opening fee, 6002-Closing fee, 6003-Overnight interest, 6004-Market closing profit and loss, 6005-Stop loss closing profit and loss, 6006-Stop profit closing profit and loss, 6007-System forced liquidation profit and loss, 6008-Expiration forced liquidation profit and loss, 6009-Manual forced liquidation profit and loss, 36001-Transferred amount, 36002-Transferred out Amount, 42001-issuing rewards, 42002-rebating rewards, 42003-issuing rebates, 42004-rebating rebates]; Contract warehouse type: [7001-front-end deposit, 7002-deposit fee, 8001-front-end withdrawal, 8002-cancel withdrawal, 8003-withdrawal fee, 8004-cancel fee, 8005-confirm transfer, 9001-system clearing, 10001-quota adjustment deposit, 10002-quota adjustment withdrawal 10003-Quota Adjustment Others, 10004-Quota Adjustment Bonus, 10005-Quota Adjustment Released and Unwithdrawable, 10006-Quota Adjustment Unwithdrawable, 10007-Quota Adjustment Transferred to Rebate, 11001-Freeze, 11002-Unfreeze, 12001-Transfer Opening Margin, 12002-Opening Fee, 12003-Release Closing Margin, 12004-Closing Fee, 12005-Overnight Interest, 12006-Market Price Flat Position profit and loss, 12007-profit and profit and loss of stop-profit closing, 12008-profit and loss of stop-loss closing, 12009-system forced liquidation profit and loss, 120010-profit and loss of forced liquidation at expiration, 120011-manual forced liquidation profit and loss, 13001-manual increase in margin, 13002-manual reduction in margin, 37001-amount transferred in, 37002-amount transferred out, 43001-issuance of rewards, 43002-rebate of rewards, 43003-issuance of rebates, 43004-rebate Rebate]; Leverage type: [14001-front-end deposit, 14002-deposit fee, 15001-front-end withdrawal, 15002-cancel withdrawal, 15003-withdrawal fee, 15004-cancel fee, 15005-confirm transfer, 16001-quota adjustment deposit, 16002-quota adjustment withdrawal, 16003-quota adjustment other, 16004-quota adjustment bonus, 16005-quota adjustment release cannot be withdrawn, 16006- The credit limit adjustment cannot be withdrawn, 16007-credit limit adjustment transfer to rebate, 17001-freeze, 17002-unfreeze, 18001-incoming amount, 18002-outgoing amount, 18003-automatic loan handling fee, 18004-automatic repayment handling fee, 18005-ordinary handling fee, 19001-loan principal, 20001-loan principal, 21001-repayment principal, 21002-repayment interest, 22001-repayment principal, 2200 2-Repayment interest, 23001-Loan interest, 35001-Repayment principal, 35002-Repayment interest, 38001-Inward amount, 38002-Outward amount, 40001-Forced liquidation to return principal, 40002-Forced liquidation to return interest, 44001-Issuance of rewards, 44002-Reduction of rewards, 44003-Issuance of rebates, 44004-Reduction of rebates]; Spot leverage matching: [50001-Front-end deposit, 50002-Deposit procedures Fee, 51001-front-end withdrawal, 51002-cancel withdrawal, 51003-withdrawal fee, 51004-cancel fee, 51005-confirm transfer, 52001-quota adjustment deposit, 52002-quota adjustment withdrawal, 52003-quota adjustment other, 52004-quota adjustment bonus, 52005-quota adjustment release cannot be withdrawn, 52006-quota adjustment cannot be withdrawn, 52007-quota adjustment transfer rebate, 53001-freeze, 53002-thaw, 54001- amount of money deposited, 54002- amount of money withdrawn, 54003- transaction fee, 55001- amount of money transferred in, 55002- amount of money transferred out, 59001- reward issuance, 59002- reward deduction, 59003- rebate issuance, 59004- rebate deduction]; Stock category [60101- front-end deposit, 60102- deposit fee, 60201- front-end withdrawal, 60202- withdrawal cancellation, 60203- withdrawal fee, 60204- cancellation fee, 60205-confirm transfer, 60301-quota adjustment deposit, 60302-quota adjustment withdrawal, 60303-quota adjustment other, 60304-quota adjustment bonus, 60305-quota adjustment release cannot be withdrawn, 60306-quota adjustment_cannot be withdrawn, 60307-transfer rebate, 60401-freeze, 60402-unfreeze, 60501-collateral freeze, 60502-collateral unfreeze, 60601-transaction amount, 60602-transaction amount, 6 0603-Transaction Fee, 60701-Automatic Borrowing, 60801-Automatic Repayment, 60802-Forced Liquidation Repayment, 60901-Amount Transferred In, 60902-Amount Transferred Out, 61001-Margin Trading Interest Calculation, 61101-Margin Trading Interest Settlement, 61201-Reward Issuance, 61202-Reward Rebate, 61203-Rebate Commission Issuance, 61204-Rebate Commission Rebate, 61301-System Clearance, 61401-Dividend Amount, 61402-Dividend Fee】)
"companyId": 21,// Company ID
"createTime": 1658739568400,// Creation time
"currency": 66,// Currency asset ID
"currencyCode": "HKD",// Currency code
"customerId": 21880,// Customer ID
"customerNo": "86000004",// Customer number
"digits": 5,// Amount decimal place book
"id": "0",// Record ID
"orderId": 10101,// Transaction order ID
"remark": "ryder_test",// Remark
"status": 2,// Status
"subjectId": 667,// Subject ID
"subjectType": 1,// Account type (1-balance, 2-freeze, 3-available, 4-liability balance, 5-liability frozen, 6-liability available, 7-freeze available, 8-freeze available-freeze, 9-freeze available, 10-platform balance, 11-platform frozen, 12-platform available, 13-institutional fund balance, 14-institutional fund frozen, 15-institutional fund available, 16-payable withdrawal balance, 17-payable withdrawal fund frozen, 18-payable withdrawal available, 19-occupied margin balance, 20-occupied margin frozen, 21-occupied margin available, 22-interest balance, 23-interest frozen, 24-interest available, 25-collateral balance, 26-collateral frozen, 27-collateral available)
"tradeType": 6, // Game type
"updateTime": 1658739568502, // Update time
"version": 0 // Version number
},
"eventType": "subject_water_insert"
}
```

### Account change details update (subject\_water\_update)

```json
{
"data": {
"accountId": 1000087,// Account id
"accountType": 1,//Account type
"amountAfter": 11210000000,//Amount after update
"amountIn": 11210000000,//Account deposit amount
"amountOut": 11210000000,//Account withdrawal amount
"bookkeepId": 2022072500115,//Voucher record id
"businessType": 603,// Business type (Full-position contract type [1-Deposit, 2-Withdrawal, 3-System clearing, 4-Quota adjustment, 5-Freeze, 6-Trading, 36-Transfer, 42-Reward]; Single-position contract type: [7-Deposit, 8-Withdrawal, 9-System clearing, 10-Quota adjustment, 11-Freeze, 12-Trading, 13-Adjust margin, 37-Transfer, 43-Reward]; Leverage type: [14-Deposit, 15-Withdrawal, 16-Quota adjustment, 17-Freeze, 18-Trading, 19-Automatic borrowing, 20-Manual borrowing, 21-Automatic repayment, 22-Manual repayment, 23-Loan interest interest, 35-background repayment, 38-transfer, 40-forced liquidation repayment, 44-reward]; spot leverage matching: [50-deposit, 51-withdrawal, 52-quota adjustment, 53-freeze, 54-trading, 55-transfer, 59-reward]; stock [601-deposit, 602-withdrawal, 603-quota adjustment, 604-freeze, 605-collateral, 606-trading, 607-loan, 608-repayment, 609-transfer, 610-interest calculation, 611-interest settlement, 612-reward, 613-system clearing, 614-company action])
"businessType1": 60301,// Sub-business type (Full-position contract type [1001-Front-end deposit, 1002-Deposit fee, 2001-Front-end withdrawal, 2002-Cancel withdrawal, 2003-Withdrawal fee, 2004-Cancel fee, 2005-Confirm transfer, 3001-System clear, 4001-Quota adjustment deposit, 4002-Quota adjustment withdrawal, 4003-Quota adjustment other, 4004-Quota adjustment bonus, 4005-Quota adjustment release cannot be withdrawn, 4006-Quota adjustment cannot be withdrawn, 4007-Quota adjustment transfer rebate, 5001-Freeze, 5002-Unfreeze, 6001-Opening fee, 6002-Closing fee, 6003-Overnight interest, 6004-Market closing profit and loss, 6 ... -Stop loss profit and loss, 6006-Stop profit profit and loss, 6007-System forced liquidation profit and loss, 6008-Expiration forced liquidation profit and loss, 6009-Manual forced liquidation profit and loss, 36001-Transferred amount, 36002-Transferred amount, 42001-Reward issuance, 42002-Reward deduction, 42003-Rebate issuance, 42004-Rebate deduction]; Contract position-by-position: [7001-Front-end deposit, 7002-Deposit fee, 8001-Front-end withdrawal, 8002-Cancel withdrawal, 8003-Withdrawal fee, 8004-Cancel fee, 8005-Confirm transfer, 9001-System clearing, 10001-Quota adjustment deposit, 10002-Quota adjustment withdrawal, 10003-Quota adjustment other He, 10004- quota adjustment bonus, 10005- quota adjustment release cannot be withdrawn, 10006- quota adjustment cannot be withdrawn, 10007- quota adjustment transfer to rebate, 11001-freeze, 11002-unfreeze, 12001-transfer opening margin, 12002-opening fee, 12003-release closing margin, 12004-closing fee, 12005-overnight interest, 12006-market closing profit and loss, 12007-stop profit closing profit and loss, 12008-stop loss closing profit and loss, 12009-system forced liquidation profit and loss, 120010-expiration forced liquidation profit and loss, 120011-manual forced liquidation profit and loss, 13001-manual increase in margin, 13002-manual reduction in margin, 37001-transferred amount, 37002-transferred amount, 43001-reward issuance, 43002-reward deduction, 43003-rebate issuance, 43004-rebate deduction]; Leverage type: [14001-front-end deposit, 14002-deposit fee, 15001-front-end withdrawal, 15002-cancel withdrawal, 15003-withdrawal fee, 15004-cancel fee, 15005-confirm transfer, 16001-quota adjustment deposit, 16002-quota adjustment withdrawal, 16003-quota adjustment other, 16004-quota adjustment bonus, 16005-quota adjustment release cannot be withdrawn, 16006-quota adjustment cannot be withdrawn, 16007-quota adjustment transfer rebate, 1 7001-freeze, 17002-unfreeze, 18001-incoming amount, 18002-outgoing amount, 18003-automatic loan handling fee, 18004-automatic repayment handling fee, 18005-ordinary handling fee, 19001-loan principal, 20001-loan principal, 21001-repayment principal, 21002-repayment interest, 22001-repayment principal, 22002-repayment interest, 23001-loan interest, 35001-repayment principal, 35002-repayment interest, 38001-incoming amount, 38002-outgoing amount, 40001-forced liquidation to return principal, 40002-forced liquidation to return interest, 44001-issuance of rewards, 44002-refund of rewards, 4 4003-Issuing rebates, 44004-Deducting rebates]; Spot leverage matching: [50001-Front-end deposits, 50002-Deposit fees, 51001-Front-end withdrawals, 51002-Cancel withdrawals, 51003-Withdrawal fees, 51004-Cancel fees, 51005-Confirm transfers, 52001-Quota adjustment deposits, 52002-Quota adjustment withdrawals, 52003-Quota adjustment others, 52004-Quota adjustment bonuses, 52005-Quota adjustment release cannot be withdrawn, 52006-Quota adjustment cannot be withdrawn, 52007-Quota adjustment transfer rebates, 53001-Freeze, 53002-Unfreeze, 54001-Incoming amount, 54002-Outgoing amount, 54 003-Transaction fee, 55001-Deposit amount, 55002-Debit amount, 59001-Reward issuance, 59002-Reward deduction, 59003-Rebate issuance, 59004-Rebate deduction]; Stock category [60101-Front-end deposit, 60102-Deposit fee, 60201-Front-end withdrawal, 60202-Cancel withdrawal, 60203-Withdrawal fee, 60204-Cancel fee, 60205-Confirm transfer, 60301-Quota adjustment deposit, 60302-Quota adjustment withdrawal, 60303-Quota adjustment other, 60304-Quota adjustment bonus, 60305-Quota adjustment release cannot be withdrawn, 60306-Quota adjustment_cannot be withdrawn, 60307 - Transfer to rebate, 60401-freeze, 60402-unfreeze, 60501-freeze collateral, 60502-unfreeze collateral, 60601-transaction amount, 60602-transaction amount, 60603-transaction fee, 60701-automatic loan, 60801-automatic repayment, 60802-forced liquidation repayment, 60901-transferred amount, 60902-transferred amount, 61001-margin trading interest calculation, 61101-margin trading interest settlement, 61201-reward issuance, 61202-reward deduction, 61203-rebate issuance, 61204-rebate deduction, 61301-system clearing, 61401-dividend amount, 61402-dividend fee])
"companyId": 21,// Company ID
"createTime": 1658739568400,// Creation time
"currency": 66,// Currency asset ID
"currencyCode": "HKD",// Currency code
"customerId": 21880,// Customer ID
"customerNo": "86000004",// Customer number
"digits": 5,// Amount decimal place book
"id": "0",// Record ID
"orderId": 10101,// Transaction order ID
"remark": "ryder_test",// Remark
"status": 2,// Status
"subjectId": 667,// Subject ID
"subjectType": 1,// Account type (1-balance, 2-freeze, 3-available, 4-liability balance, 5-liability frozen, 6-liability available, 7-freeze available, 8-freeze available-freeze, 9-freeze available, 10-platform balance, 11-platform frozen, 12-platform available, 13-institutional fund balance, 14-institutional fund frozen, 15-institutional fund available, 16-payable withdrawal balance, 17-payable withdrawal fund frozen, 18-payable withdrawal available, 19-occupied margin balance, 20-occupied margin frozen, 21-occupied margin available, 22-interest balance, 23-interest frozen, 24-interest available, 25-collateral balance, 26-collateral frozen, 27-collateral available)
"tradeType": 6, // Game type
"updateTime": 1658739568502,//Update time
"version": 0// Version number
},
"eventType": "subject_water_update"
}
```

### Add position information (position\_insert)

Description: symbolDigits is used for costPrice, openPrice and other price-related information. currencyDigits is used for closeFee, openFee and other procedures. openVolume=contractSize\*number of lots.

```json
{
"data": {
"accountId": 1000091,//Trading account id
"bizType": 2,// Opening business type. Play 1 (1-market opening; 2-market closing; 3-stop loss closing order; 4-take profit closing order; 5-forced liquidation order for liquidation; 6-expiration closing order; 7-account closing order; 8-manual forced liquidation order; 10-limit price pre-buried order; 11-stop loss pre-buried order; 12-limit opening;); Play 2 (1-market opening; 2-market closing; 3-stop loss closing order; 4-take profit closing order; 5-forced liquidation order for liquidation; 6-expiration closing order; 7-account closing order; 8-manual forced liquidation order; 10-limit price pre-buried order; 11-stop loss pre-buried order; 13-matching limit opening order; 14-matching limit closing order;);
"closeFee": 0, //Closing fee
"collatrealFrozen": 0, //Collateral amount
"companyId": 21, //Company id
"contractSize": 1, // Contract size
"costPrice": 10157, // Cost price
"createBy": 1000091, // Creator id
"createTime": 1658815815134, // Creation time
"currency": "HKD", // Asset code
"currencyDigits": 5, // Asset decimal places
"customerGroupId": 3, // Customer group id
"customerId": 21882, // Customer id
"customerNo": "86000006", // Customer number
"dealId": 423, // Transaction record id
"direction": 1, // Transaction direction
"id": "2022072600132", // Position record id
"openFee": 0, // Opening fee
"openMargin": 0, // Opening margin
"openPrice": 0, // Opening price
"openVolume": 36.0, // Opening quantity
"orderId": 322, // Trading order id
"status": 1, // Position status 1- Opening; 2- Completed; 3- Partially closed;
"symbolDigits": 2, // Product decimal places
"symbolId": 179, // Trading product id
"tradeModel": 1, // Transaction mode
"tradeType": 6, // Game type
"interest":"0", // Interest to be collected. Game 2 is useful
"openTradeAmount":"100", // Opening transaction amount
"lockNum":"0", // Locked position quantity. Game 2 is useful
"crossLevelNum":1, // Leverage multiple
"currentTradeAmount":"100", // Current transaction amount
"maintenanceMargin":"10", // Maintenance margin. Useful for Play 2
"marginSetType":"1", // Margin type. 1-Ratio; 2-Range;
"occupyTheMargin":"100", // Occupied margin. Useful for Play 2
"singleMargin":"10", // Unit margin. Useful for Play 2
"takeProfit":"0", // Take Profit unit price, integer, needs to be processed with product decimals
"stopLoss":"0", // Stop Loss unit price, integer, needs to be processed with product decimals
"warningMargin":"0", // Warning margin. Useful for gameplay 2
"updateBy": 1000091, // Updater id
"updateTime": 1658815815136 // Update time
},
"eventType": "position_insert"
}
```

### Position information update (position\_update)

```
{
"data": {
"accountId": 1000091, // Trading account id
"bizType": 2, // Opening business type. Play 1 (1-market opening; 2-market closing; 3-stop loss closing order; 4-take profit closing order; 5-forced liquidation order for liquidation; 6-expiration closing order; 7-account closing order; 8-manual forced liquidation order; 10-limit price pre-buried order; 11-stop loss pre-buried order; 12-limit opening;); Play 2 (1-market opening; 2-market closing; 3-stop loss closing order; 4-take profit closing order; 5-forced liquidation order for liquidation; 6-expiration closing order; 7-account closing order; 8-manual forced liquidation order; 10-limit price pre-buried order; 11-stop loss pre-buried order; 13-matching limit opening order; 14-matching limit closing order;);
"closeFee": 0, //Closing fee
"collatrealFrozen": 0, //Collateral amount
"companyId": 21, //Company id
"contractSize": 1, // Contract size
"costPrice": 10157, // cost price
"createBy": 1000091, // creator id
"createTime": 1658815815134, // creation time
"currency": "HKD", // asset code
"currencyDigits": 5, // asset decimal places
"customerGroupId": 3, // customer group id
"customerId": 21882, // customer id
"customerNo": "86000006", // customer number
"dealId": 423, // transaction record id
"direction": 1, // transaction direction
"id": "2022072600132", // position record id
"openFee": 0, // opening fee
"openMargin": 0, // opening margin
"openPrice": 0, // opening price
"openVolume": 36.0, // Opening volume
"orderId": 322, // Trading order id
"status": 1, // Position status 1- Opening; 2- Completed; 3- Partially closed;
"symbolDigits": 2, // Product decimal places
"symbolId": 179, // Trading product id
"tradeModel": 1, // Transaction model
"tradeType": 6, // Game type
"interest":"0", // Interest to be collected. Game 2 is useful
"openTradeAmount":"100", // Opening transaction amount
"lockNum":"0", // Locked position quantity. Game 2 is useful
"crossLevelNum":1, // Leverage multiple
"currentTradeAmount":"100", // Current transaction amount
"maintenanceMargin":"10", // Maintenance margin. Useful for Play 2
"marginSetType":"1", // Margin type. 1-Ratio; 2-Range;
"occupyTheMargin":"100", // Occupied margin. Useful for Play 2
"singleMargin":"10", // Unit margin. Useful for Play 2
"takeProfit":"0", // Take Profit unit price, integer, needs to be processed with product decimals
"stopLoss":"0", // Stop Loss unit price, integer, needs to be processed with product decimals
"warningMargin":"0", // Warning margin. Play method 2 is useful
"updateBy": 1000091, // Updater id
"updateTime": 1658815815136 // Update time
},
"eventType": "position_update"
}
```

### Delete position information (position\_delete)

```
{
"data": {
"id": "2022072600132", // Position record id
"companyId": 21 // Company id
"accountId": 1000091, // Trading account id
"bizType": 2, // Opening business type. Play 1 (1-market opening; 2-market closing; 3-stop loss closing order; 4-take profit closing order; 5-forced liquidation order for liquidation; 6-expiration closing order; 7-account closing order; 8-manual forced liquidation order; 10-limit price pre-buried order; 11-stop loss pre-buried order; 12-limit opening;); Play 2 (1-market opening; 2-market closing; 3-stop loss closing order; 4-take profit closing order; 5-forced liquidation order for liquidation; 6-expiration closing order; 7-account closing order; 8-manual forced liquidation order; 10-limit price pre-buried order; 11-stop loss pre-buried order; 13-matching limit opening order; 14-matching limit closing order;);
"closeFee": 0, //Closing fee
"collatrealFrozen": 0, //Collateral amount
"companyId": 21, //Company id
"contractSize": 1, // Contract size
"costPrice": 10157, // cost price
"createBy": 1000091, // creator id
"createTime": 1658815815134, // creation time
"currency": "HKD", // asset code
"currencyDigits": 5, // asset decimal places
"customerGroupId": 3, // customer group id
"customerNo": "86000006", // customer number
"dealId": 423, // transaction record id
"direction": 1, // transaction direction
"openFee": 0, // opening fee
"openMargin": 0, // opening margin
"openPrice": 0, // opening price
"openVolume": 36.0, // opening quantity
"orderId": 322, // transaction order id
"status": 1, // position status 1-holding; 2-completed; 3-partially closed;
"symbolDigits": 2, // product decimal places
"symbolId": 179, //Trading product id
"tradeModel": 1, // Transaction model
"tradeType": 6, // Game type
"interest":"0", // Interest to be collected. Useful for Game 2
"openTradeAmount":"100", // Opening transaction amount
"lockNum":"0", // Locked position quantity. Useful for Game 2
"crossLevelNum":1, // Leverage multiple
"currentTradeAmount":"100", // Current transaction amount
"maintenanceMargin":"10", // Maintenance margin. Useful for Game 2
"marginSetType":"1", // Margin type. 1-Ratio; 2-Range;
"occupyTheMargin":"100", // Occupied margin. Useful for Game 2
"singleMargin":"10", // Unit margin. Play method 2 is useful
"takeProfit":"0", // Take profit unit price, integer, needs to be processed with product decimals
"stopLoss":"0", // Stop loss unit price, integer, needs to be processed with product decimals
"warningMargin":"0", // Warning margin. Play method 2 is useful
"updateBy": 1000091, // Updater ID
"updateTime": 1658815815136 // Update time
},
"eventType": "position_delete"
}
```

### Transaction (trade\_deal)

```json
{
"data":{
"accountDigits":4, //Account decimal places, transaction amount, decimal places
"accountId":1269478, //Deposit account ID
"bizType":1, //Business type
"companyId":362, //Company ID
"contractSize":1, //Product contract size
"convertExchangeRate":1, //Exchange rate for converting handling fee currency to USDT
"convertFee":9028, //Value after handling fee is converted to USDT
"convertFeeDigits":4, //Decimal places after handling fee is converted to USDT
"createTime":1689658686940, // creation time
"customerGroupId":1, // customer group id
"customerId":15115, // customer id
"customerNo":"86015114", // customer number
"digits":2, // average transaction price decimal places
"direction":1, // buy and sell direction, 1 buy 2 sell
"executeMargin":768339, // opening margin
"executeMarginCategoryId":3, // margin category id
"executeNum":0.001, // number of transactions
"executePrice":3009452, // transaction price
"executeTime":1689658687260, // transaction time
"fee":9028, // handling fee
"feeDigits":4, // handling fee decimal places
"id":"1822307", // transaction record id
"orderId":1822307, // Order record id
"orderStatus":2, // Order status
"pointRatio":1, // Point ratio
"positionId":2023071846555,
"spread":3251, // Spread
"symbolId":706, // Product id
"symbolName":"BINAN_BTC_USDT11", // Product name
"tradeType":1, // Trading modes 1, 2, and 5 are full-margin contracts, fixed-margin contracts, and spot contracts.
"pnl":1212, // Close profit and loss, decimal places are the same as the account decimal places, tradeTpe is 1 and 2, bizType is 2, 3, 4, 5, 6, 7, 8 when there is a value, currency is the same as the account currency, obtained by accountId association query
"source":"H5",//H5: mobile web; PC_Web: pcweb; System: system; Android: Android native app; iOS: Apple native app; HOS: Hongmeng OS; PC_Win: pcwindows client; PC_Mac: pcmac client; default is the same as the login source. (limited to 255 characters, enumeration is for reference only, only letters, numbers, and underscores can be used)
"thirdPartyOrder":"",//third-party order identification, (limited to 255 characters, only letters, numbers, and underscores can be used)
"updateTime":1689658687263
},
"eventType":"trade_deal"
}
```

### Deposit successful (deposit)

```json
{
"data": {
"accountId": 1000077, // Deposit account id
"actualAmount": 50.000000000, // Actual deposit amount
"blockchainName": "", // Encrypted acquisition chain name
"checkStatus": 2, // Review status
"companyId": 1, // Company id
"country": "CN", // Customer country code
"createBy": "86000000", // Creator
"createTime": 1647310213627, // Create actual
"customerNo": "86000000", // Customer number
"depositCurrency": "USDT", // Deposit currency
"depositFee": 0, // Deposit fee
"depositFrom": "H5", // Source of deposit (terminal type H5_Android, H5_IOS, PCUI_Windows, PCUI_Mac, APP_Android, APP_IOS)
"depositStatus": 2, // Deposit status
"finalAmount": 50.000000000, // Final amount
"fromPaymentAmount": 343.500000000, // Channel notification amount
"id": "89", // Proposal record id
"intendAmount": 50.000000000, // Proposal amount (amount received by the platform)
"notifyStatus": false, // Payment channel notification status
"paymentChannelClientType": "mobile", // Client type pc, mobile
"paymentCode": "mdpay", // Payment channel code
"paymentCurrency": "CNY", // Deposit currency (currency supported by the payment channel)
"paymentStatus": 1, // Payment status, pending payment: 1, payment successful: 2, payment failed: 3
"paymentType": "bank", // payment channel type
"proposalNo": "D2022031522005", // proposal number
"queryMaxCount": 20, // maximum number of queries
"revision": 3, // data version number
"toPaymentAmount": 343.500000000, // amount sent to the payment platform (amount received by the payment channel)
"toPaymentRate": 6.870000000, // deposit exchange rate used by the payment platform
"tradeType": 5, // gameplay type
"updateBy": "admin", // updater
"updateTime": 1647310473479 // actual update
},
"eventType": "deposit"
}
```

### Adjustment of quota (account\_adjust)

```
{
"data": {
"accountCurrency": "HKD", // Account currency (trading account currency)
"accountId": 1006333, // Trading account ID
"amount": 1000000.000000000, // Proposal amount
"businessType": 60301, // Business type code
"checkBy": "admin", // Approver
"checkStatus": 2, // Proposal status, waiting for manual approval: 1, Approval successful: 2, Approval failed: 3
"companyId": 401, // Company id
"createBy": "admin", // Creator (Applicant)
"createTime": 1670815268755, // Creation time (application time)
"customerNo": "86001385", // Customer account
"id": "212", // Primary key id
"proposalNo": "A20221212686244",// Proposal No.
"revision": 2, // Optimistic lock
"tradeType": 6, // Game type
"updateBy": "admin", // Updater
"updateTime": 1670815269000, // Update time
"withdraw": false // Can withdraw
},
"eventType": "account_adjust"
}
```

### Add and update withdrawal proposals (withdraw)

```
{
"data": {
"id": "212", // Primary key id
"companyId": 401, // Company id
"proposalNo": "A20221212686244",// Proposal No.
"customerNo": "86001385", // Customer number
"accountCurrency": "HKD", // Account currency (trading account currency)
"withdrawCurrency":"HKD",//Withdrawal currency (currency supported by payment channel)
"accountId": 1006333, // Trading account ID
"tradeType": 6, // Game type
"country": "CN", // Country
"amount": 1000000.000000000, // Proposal amount
"rate": 1, // Withdrawal exchange rate sent to platform CATS2
"withdrawFee": 0, // Withdrawal fee
"finalAmount": 1000000, // Final withdrawal amount
"bankName": "", // Bank card bank name
"bankCardNo": "", // Bank card number
"bankAccountName": "", // Bank card holder name
"checkStatus": 2, // Proposal status, waiting for manual approval: 1, Approval successful: 2, Approval failed: 3
"transferStatus": 2,// Transfer status, pending transfer: 1, successful transfer: 2, failed transfer: 3
"checkBy": "admin", // approver
"remark": "admin", // remarks
"withdrawType": 1, // withdrawal type, cash withdrawal: 1 (withdraw to bank card), coin withdrawal: 2 (withdraw digital currency to digital wallet)
"withdrawCoinStatus": 1, // coin withdrawal status, pending coin withdrawal: 1, successful coin withdrawal: 2, failed coin withdrawal: 3, failed submission: 4
"withdrawMethod": "bank", // withdrawal method, corresponding bank card: bank, corresponding digital wallet: digit_wallet, skrill electronic wallet: skrill_wallet, wire transfer: wire
"blockchainName": null, // chain name, data dictionary configuration, the payment method is a digital wallet, display the corresponding chain name (also called transfer network), such as Omin, ERC20, TRC20
"thirdMessage": "admin", // call third-party response message
"txid": null, // txid
"rawAmount":0, // Original amount
"createBy": "admin", // Creator (applicant)
"createTime": 1670815268755, // Creation time (application time)
"revision": 2, // Optimistic
"updateBy": "admin", // Updater
"updateTime": 1670815269000, // Update time
"withdraw": false // Can withdraw
},
"eventType": "withdraw"
}
```
