---
icon: message-dots
---

# Custom message API

## Custom API

Message open interface, white label docking instructions

### Applicable scene

* For the sending channels (email, SMS) that MultiMarket does not support, the white label can connect to the sending channel by itself and provide an external interface to connect with MultiMarket. The MultiMarket platform will call this interface according to the specifications of this document;
* MultiMarket provides a set of interface docking APIs. White labels need to provide interfaces according to this specification. The API specifications are detailed below.
* Then, on the white label management backend page (SMS account, email account page), select "Custom" when adding a new account, and configure the interface URL and public key (for authentication).

### Public and private key rules

Asymmetric encryption algorithm: RSA algorithm, key length: 1024.

Example：&#x20;

{% code title="" overflow="wrap" %}
```javascript
public key：MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCa7PS812qm7RMiONbErVCl7fjNtb1gYgQOsaxVOmp/wa0EH8W8QZ3VrtzwF9FbPe9crtES5RHUkV4LNaApk+WDnF6dQ217UnC+S2wb30S7rPMtHBi7DeyRfOqZkDGbsonTM0WW/WMM2eHNBbF4rfAKImzFe2ZkAl2GMHzHXc4aVQIDAQAB

private key：
MIICdgIBADANBgkqhkiG9w0BAQEFAASCAmAwggJcAgEAAoGBAJrs9LzXaqbtEyI41sStUKXt+M21 vWBiBA6xrFU6an/BrQQfxbxBndWu3PAX0Vs971yu0RLlEdSRXgs1oCmT5YOcXp1DbXtScL5LbBvf RLus8y0cGLsN7JF86pmQMZuyidMzRZb9YwzZ4c0FsXit8AoibMV7ZmQCXYYwfMddzhpVAgMBAAEC gYAo3sP9oXKQUNCQYaA+yF4TOAE/+2bXK2RYoASPg1afF2/WO6+FZ2YE/hlo+U+Qm3ku4StkqauX gTXnDSGQdmTAdxh9YO3Aj81qn6VK6tlGkzWcKfcO+NqNyp3AwfF9aSackBi/rLH8GNNQZtoNBy8z Q6KBD2sQQRITuMu7hi4VwQJBANoY3Fi9rIgs3t4JifVMtyZC6Fpi9bEoCLEizZchwTr24P4mcbni 4uV9O0mI9OaqI9nAlet0KVhRaoMxi/ES2nECQQC12ZhxVzHe+wfCyyx/fPMXSr7cwmM1F3lk5IRa /hCXpVc9ncd/n12TNS7lJwVhqc+tBhWP6i3PSEH0hiyp0QglAkEAh/WNj4iWgMGwIazCovezCRgW rxoX3dt+J6bxkTCKvA5hTi57IQ1usu9xwTKusQkJllp3WzOr/pGqm6SMf7loEQJAbf6dJ8lfIAnl atzsIH0aqPcMNYna6i01v2I98LAGp0NaXqnGFxr1ReqAYBlXNvi45mZsum0iomOJiXdzIpCOhQJA AoXt2DlMSrXGIM0j/j56jUKOH0DNsadGned6SORnBiPjGr38eZwTxAIkxsoaPXS+9XJcQ5neWkwc 46caWU1H1Q==
```
{% endcode %}

### API Specifications

* Our calling method is http post
* The parameters use the json format.
* Parameters need to be authenticated

The following details the parameters of SMS and email, as well as the authentication method.

***

* Email Parameters

{% code title="" overflow="wrap" %}
```json
{
    "pushType":"whatapp",
    "pushId":"whatapp user id",
    "toUser":"18321956010@163.com",
    "trace":"aaaaaaaaaabbbbbbbbbb11111",
    "sign":"Zni/VixZVrxAt2GzIgRetSFub4Kk1C7JQsURlbXDJmHllv4Vr1SfJC66dnk0OPdylf4qlT9UQle+pAcbNKEBjMHkgeucaAG82syPNi18StNTWx+DNPvl1VvUGGJQQw6I7QClaEIefccyXUDqW78+gEIq8i5VNm/eop0bBoPu8Ao=",
    "title":"Verification Code",
    "content":"【XXXX】Your verification code is 847999。",
    "timestamp":1651118320014
}
```
{% endcode %}

Parameter Description

| parameter | type   | required     | describe                                      |
| --------- | ------ | ------------ | --------------------------------------------- |
| pushType  | String | Not required | Information push channel type                 |
| pushId    | String | Not required | Information push account ID                   |
| toUser    | String | required     | Email Recipient                               |
| trace     | String | required     | Global link unique identifier                 |
| sign      | String | required     | sign                                          |
| title     | String | required     | title                                         |
| content   | String | required     | content                                       |
| timestamp | long   | required     | Request sending time, timestamp, milliseconds |

* SMS parameters

{% code title="" overflow="wrap" %}
```json
{
    "pushType":"whatapp",
    "pushId":"whatapp user id",
    "toUser":"18321956010",
    "trace":"aaaaaaaaaabbbbbbbbbb11111",
"sign":"Zni/VixZVrxAt2GzIgRetSFub4Kk1C7JQsURlbXDJmHllv4Vr1SfJC66dnk0OPdylf4qlT9UQle+pAcbNKEBjMHkgeucaAG82syPNi18StNTWx+DNPvl1VvUGGJQQw6I7QClaEIefccyXUDqW78+gEIq8i5VNm/eop0bBoPu8Ao=",
    "content":"【XXXX】Your verification code is 847999。",
    "timestamp":1651118320014
}
```
{% endcode %}

Parameter Description

| parameter | type   | required     | describe                                      |
| --------- | ------ | ------------ | --------------------------------------------- |
| pushType  | String | Not required | Information push channel type                 |
| pushId    | String | Not required | Information push account ID                   |
| toUser    | String | required     | SMS recipient                                 |
| trace     | String | required     | Global link unique identifier                 |
| sign      | String | required     | sign                                          |
| content   | String | required     | content                                       |
| timestamp | long   | required     | Request sending time, timestamp, milliseconds |

* Authentication

1. Decrypt the request parameter sign and record the result as signContent: 1) Get the value of the sign field from the request parameter, record it as data; 2) Use your own private key, record it as privateKey; 3) Decode data and privateKey by base64: Base64.decodeBase64(data), Base64.decodeBase64(privateKey); 4) Use the two data decoded by base64 in the previous step to perform RSA decryption to obtain a byte array, convert it to String, record it as signContent;
2. According to the request parameters, get the encrypted original text, recorded as signContentSource 1) Encrypted original text of email: signContentSource=toUser@timestamp@trace; 1) Encrypted original text of SMS: signContentSource=toUser@timestamp@trace;
3. Compare the encrypted original text (signContentSource) and the decrypted result (signContent): if they are equal, authentication is successful.

Successful response data

```json
{
    "msg":"success",
    "code":"200"
}
```
