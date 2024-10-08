---
icon: readme
---

# Introduction



This document explains how to embed the trading UI into the main business system. Through the main business system, users can directly jump to or open the trading system using an embedded iframe, and perform product transactions without needing to log in again.

\


Process:

1\. When the main business system jumps to the trading system, it needs to pre-check whether the user's account exists. If it doesn't exist, registration is required.

2\. After registration, obtain the user's account and bind it with the main account. The next time the user opens the trading system, they will exchange for a token.

3\. If the user has already been bound, use the account and password to obtain a valid token.

4\. Based on the valid token, the trading system address is concatenated and opened with an iframe.

5\. At this point, the trading UI will internally log in automatically using the valid token, and product transactions can be performed once the page is opened.
