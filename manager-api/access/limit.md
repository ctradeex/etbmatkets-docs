# Limit

## Speed ​​Limit&#x20;

MultiMarkets aims to provide a stable and secure platform for all users at all times. Therefore, all parties continuously monitor traffic to identify patterns that could negatively impact the network.

If the traffic from a single account is identified as too high and the rate limit is reached, MultiMarkets may temporarily throttle or restrict that account. You have a rate limit on a per API endpoint and per minute basis.

If your rate limit is reached, you will see an HTTP 429 error response letting you know that your rate limit has been temporarily exceeded.

Partners should handle HTTP 429 status codes gracefully and drop and/or retry requests accordingly.

The following headers are returned with every request. If a less restrictive rate limit is required, please contact your implementation manager to determine your use case. Please note that increasing the rate limit may incur additional charges.



## Parameters&#x20;

The response header returned by the interface will include the following three fields, which respectively represent: x-ratelimit-limit represents the total number of calls that can be made in the current cycle, x-ratelimit-remairing represents the number of remaining calls in the current cycle, and x-ratelimit-reset represents the cycle time in seconds.&#x20;

> x-ratelimit-limit: 300&#x20;
>
> x-ratelimit-remairing: 299&#x20;
>
> x-ratelimit-reset: 60&#x20;

The above example: indicates that the interface can be called 300 times per minute, and currently there are 299 remaining calls that can be called
