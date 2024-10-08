---
description: Message open interface, white label docking instructions
icon: screwdriver
---

# Overview



* For the sending channels (email, SMS) that MultiMarket does not support, the white label can connect to the sending channel by itself and provide an external interface to connect with MultiMarket. The MultiMarket platform will call this interface according to the specifications of this document;
* MultiMarket provides a set of interface docking APIs. White labels need to provide interfaces according to this specification. The API specifications are detailed below.
* Then, on the white label management backend page (SMS account, email account page), select "Custom" when adding a new account, and configure the interface URL and public key (for authentication).
