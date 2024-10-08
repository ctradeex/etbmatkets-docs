---
description: Management API interface authentication and authorization
icon: garage-open
---

# Authorize

## illustrate

To authorize the white label management API, you need to obtain appId and appSecret in advance. You can obtain or reset them by contacting the main label customer service. The following is the information for testing the white label.



## Test Account

```json
{
"appId": "7cb9164942caec70594e594db46de7af",
"appSecret": "33171f3e91c45e0dfbb3c9f219906471"
}
```

{% swagger src="../.gitbook/assets/MultiMarkets-BusinessAPI.openapi.en.yaml" path="/auth/admin.admin.CompanyAuthDubboService.auth" method="post" %}
[MultiMarkets-BusinessAPI.openapi.en.yaml](../.gitbook/assets/MultiMarkets-BusinessAPI.openapi.en.yaml)
{% endswagger %}



