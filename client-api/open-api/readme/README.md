# Readme

### 1. API Introduction

This API supports placing orders, receiving transaction messages, market data subscription, and other functionalities.

Supported Methods:

* Through API key: You need to use specific header parameters when calling. For details, please refer to the following documents: [Signature Rules](https://docs.multimarkets.org/client-api/open-api/sign) and [Request & Response](https://docs.multimarkets.org/client-api/open-api/request). In the "Request & Response" documentation, optional header information parameters must be referenced based on each interface's header description. If an interface's header requires a token parameter, it should be omitted and ignored.
* The Open API interface is the same as the Client open interface. The difference is that the encryption authentication method of the request is different. The Open API needs to apply for apikey and secretKey for signature access. You can refer to the detailed interface list [Client API](https://multimarkets-c-api-en.apidocumentation.com/)

Below is a guide on how to obtain an API key.

### 2. API Key Application Process

#### Method 1:

> Log in to the trading client, find "API Management" on the "My" page, and then create an ApiKey and SecretKey on the API management page. The SecretKey is only displayed once after creation (for security reasons, the system does not store it), so it needs to be kept safely.

#### Method 2:

> Apply through the Client API interface with the following steps:

**1. Log in**

Call the interface: [Login](https://docs.multimarkets.org/client-api/login) Retrieve the token from the result for future use.

**2. Apply for an API Key**

Call the interface: [Apply API](https://docs.multimarkets.org/client-api/customer/api-management/apply-api) Retrieve the apiKey and privateKey from the result and save them. These are necessary parameters for subsequent interface calls. You only need to apply for an API key once.

**3. Bind your External IP Address**

Call the interface: [Set Permissions](https://docs.multimarkets.org/client-api/customer/api-management/set-permissions) You need to bind the IP for it to be valid long-term; otherwise, the default validity period is only 90 days.
