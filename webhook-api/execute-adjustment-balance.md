---
icon: file-user
---

# Execute adjustment balance

### # External System Credit Limit Adjustment

1: When a user places an order within the TradeBoss platform, the platform sends this request to an external system. The external system must respond within 3 seconds, otherwise the TradeBoss platform will consider it as a timeout and cancel the operation. At the same time, it will also send a "Cancel external system credit limit adjustment" request to maintain data consistency with the external system.

2: It is important to note that when calling the "Cancel external system credit limit adjustment" interface, if any exceptions occur or if a correct response is not received, there will be specified retries before aborting subsequent operations.



{% swagger src="../.gitbook/assets/multimarkets-webhook.json" path="/external-system-credit-limit-adjustment" method="post" %}
[multimarkets-webhook.json](../.gitbook/assets/multimarkets-webhook.json)
{% endswagger %}
