---
description: Sign
---

# Sign

## 1. Signature

### 1.1 Signature Rules

The signature uses the SHA1WithRSA algorithm. The secretKey serves as the key for SHA1WithRSA, and the parameters in `param` + `timestamp` serve as the operating objects for SHA1WithRSA. The output obtained is the signature.

* Step 1: Retrieve the request parameters in the body, sort the parameters alphabetically, and form a string.
  * The sorting method "alphabetical order" means sorting from smallest to largest alphabetically, comparing the first letter first, if the same, compare the second letter, and so on.
  * Remove all double quotes, whether they are from field names or field values.
  * No spaces in between.
  * If the field is `null`, it is not included in the signature.
* Step 2: Retrieve the `timestamp` parameter from the request header and append it to the result of Step 1.
* Step 3: Use the secretKey to perform SHA1WithRSA on the result from Step 2 to generate the signature.

### 1.2 Signature Example

| Parameter | Value                                                                               |
| --------- | ----------------------------------------------------------------------------------- |
| companyId | 220                                                                                 |
| apiKey    | 1710e1f6b4b54c15bea72e8669966591                                                    |
| secretKey | MIICeAIBADANBgkqhkiG9w0BAQEFAASCAmIwggJeAgEAAoGBAI5WJjsBgtiuQQZDs5qe8LBDUm2ZSa4gTBJ |

Request Parameters:

{"companyId":1,"lang":"zh-CN","customerNo":"86001308"}

Calculate Signature:

* Step 1: Retrieve the request parameters in the body and sort them alphabetically to form the following string:\
  {“companyId”:1,”customerNo”:”86001308”,”lang”:”zh-CN”}
* Step 2: Retrieve the `timestamp` parameter from the request header and append it to the result of Step 1, as follows:\
  {companyId:1,customerNo:86001308,lang:zh-CN}1650361143685
* Step 3: Use the secretKey to perform SHA1WithRSA on the result from Step 2, the result is:\
  Dihl6oOt5UkaHo9sEouquP3EqbukLX2dAOoKTSGicYryTvH1m9r6vtSLHGutZn7u34/06gjhdpbXRFPdjb51GVHvG75qWXZ1P/boL89xtuja6eTEy9q/aS8R270Q1A+m/MOTxdiifCy0IByrSpCs4VJKaj2d8jlJo2GHznsH+q0=



## 2.Attachment

Java version [demo](https://github.com/CTradeExchange/sign-demo/tree/master).
