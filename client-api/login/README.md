---
description: Trading client login authorization
icon: garage-open
---

# Login

## Introduction

This interface is used to log in to the trading system when customizing the client, and to subscribe to quotes and place trading orders.



## Interface



### &#x20;Email/Mobile phone number login

{% swagger src="../../.gitbook/assets/MultiMarkets-ClientAPI.openapi.en.yaml" path="/login/customer.app.CustomerWebApiService.login" method="post" %}
[MultiMarkets-ClientAPI.openapi.en.yaml](../../.gitbook/assets/MultiMarkets-ClientAPI.openapi.en.yaml)
{% endswagger %}



### &#x20;Login with social account

{% swagger src="../../.gitbook/assets/MultiMarkets-ClientAPI.openapi.en.yaml" path="/global/customer.app.CustomerThirdLoginService.config" method="post" %}
[MultiMarkets-ClientAPI.openapi.en.yaml](../../.gitbook/assets/MultiMarkets-ClientAPI.openapi.en.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/MultiMarkets-ClientAPI.openapi.en.yaml" path="/h/com.cats.customer.api.app.CustomerThirdLoginService/googleVerify" method="post" %}
[MultiMarkets-ClientAPI.openapi.en.yaml](../../.gitbook/assets/MultiMarkets-ClientAPI.openapi.en.yaml)
{% endswagger %}

