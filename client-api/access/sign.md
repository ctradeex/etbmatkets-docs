# Sign

### Signature Rules

1\. Connector Rule:

> In the signature, an & represents a connector and not an operator.
>
> The signature rule states that the “signature” in the body is not part of the signature calculation. However, the “timestamp” in the header must be part of the body signature.

2\. Parameter Sorting:

> Sort the remaining parameters by their names in ascending dictionary order (ascending ASCII order).
>
> Only parameters with non-empty values and of number or string type are considered for the signature.
>
> Concatenate the key-value pairs in the format “key=value”. Link multiple parameters with an & to obtain a string A. Parameters with empty values are not included in the signature.

3\. Timestamp Inclusion:

> Add timestamp=TIMESTAMP\_VALUE to obtain string B.
>
> Concatenate B & A to get string C.

4\. MD5 Encryption:

> Encrypt string C using MD5 and convert all resulting letters to uppercase to obtain the final value D, which is the “signature” value.

5\. Signature Addition and Encoding:

> Add the “signature” to the body.
>
> Convert the body to JSON and then encode it to get string E.

6\. RSA Encryption:

> Encrypt string E using the company’s public key to obtain string F.
>
> If the length of F exceeds 100, encrypt F in segments of 100 using RSA and join the encrypted segments with a comma to get the final encrypted string F.

7\. Final Request Structure:

> The final request parameters should be structured as follows:

```json
//header
{
    "timestamp": 11111131331,
    "trace": "xxxxxx"
}

//body
{
    "data": F
}
```

### Signature Example：

1\. Concatenation:

> Concatenate the parameters in ascending order: a=1\&b=2\&c=3\&timestamp=11111131331 to get string A.

2\. Timestamp:

> Add timestamp: timestamp=11111131331 to get string B.

3\. Final Concatenation:

> Concatenate A and B to get string C: timestamp=11111131331\&a=1\&b=2\&c=3\&timestamp=11111131331.

4\. MD5 Encryption:

> Encrypt string C using MD5 and convert the result to uppercase to get the final signature key.

5\. JSON Encoding:

> Convert all body parameters to JSON and then encode to get string E.

6\. RSA Encryption:

> Encrypt string E using the company’s public key to get string F.
>
> If string E has a length greater than 100, segment E and encrypt each segment: RSA(E\[0-100])=E1, RSA(E\[remaining length])=E2, then concatenate E1 and E2 with a comma to obtain the final encrypted string F (F = E1,E2).

```json
//header
{
   "timestamp": 11111131331,
   "trace": "xxxxxx"
}

//body
{
   "a": 1,
   "b": 2,
   "c": "3",
   "signature": "44b3a042-dd5d-4796-92e1-651927b6ada9"
}
```



### JAVA DEMO

[https://github.com/CTradeExchange/multimarket-demo](https://github.com/CTradeExchange/multimarket-demo)
