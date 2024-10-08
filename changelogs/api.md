---
description: History API upgrade content
---

# API

## API Release Notes for 2.6.5

The interface adjustments are as follows:

> \[Client API]: Spot trading POST /global/tradeapi.app.OrderApiService.addOrder&#x20;
>
> interface adds entryType and expiryType parameters: entryType: order type. 1-by quantity; 2-by amount; (if not passed, default buy by amount, sell by quantity) expiryType: expiry type. 1-1 day; 2-7 days; 3-30 days; 4-90 days. Default 4&#x20;
>
>
>
> \[Manager API]: Quota adjustment POST /fund.admin.CustomerAdjustProposalAdminDubboService.addCustomerAdjustProposal&#x20;
>
> interface adds return proposal number



## API Release Notes for 2.6.2

> Added the contract full position MM depth transaction mode
>
> tradeapi.app.CfdMMOrderApiService.addMarketOrder



## API Release Notes for 2.4.3

> Add subscription webhook configuration function admin.admin.CompanyWebhookDubboService.subscribe
>
> When using external settlement, it is forbidden to adjust the margin and leverage multiples tradeapi.app.PositionApiService.updateCrossLevelNum tradeapi.app.PositionApiService.updateOccupyTheMargin
>
> External settlement, providing the interface customer.app.CustomerWebApiService.queryLatestBalanceOfUserAccountInExternalSystem to query the latest balance of external system accounts
>
> Support external wallet settlement tradeapi.app.OrderApiService.addMarketOrder
>
> Third-party registration, login (no mobile phone or email required) use (0.0.2) customer.app.CustomerThirdLoginService.telegramVerify



## API Release Notes for 2.4.2

> Added agent-related interfaces customer.app.CustomerWebApiService.registerOfAgentShareLink customer.app.CustomerWebApiService.queryCustomerOfAgentPage customer.app.CustomerWebApiService.registerOfAgentShareLink
>
>
>
> Social login: Added the developer ID field returned in customer.app.CustomerThirdLoginService.config





## API Release Notes for 2.3.2

> New: First time binding mobile phone email verification TG verification code customer.app.CustomerWebApiService.firstSetPhone customer.app.CustomerWebApiService.firstSetEmail customer.app.CustomerWebApiService.firstSetLoginPwd
>
> Provides the interface customer.app.CustomerWebApiService.changeCustomerAddressAndPostalCode for updating the mailing address and postal code
>
> Provides interface for querying user message language and setting message language version=0.0.1 bizType=customer.app.CustomerWebApiService.findCustomerLang
>
> Adjustment: KYC certificate validity period is randomly generated when it is not filled in customer.app.KycWebApiService.kycLevelApply customer.app.KycWebApiService.kycApply
>
> Returns the activation status customer.app.CustomerWebApiService.findCustomerInfo customer.app.CustomerWebApiService.login





## API Release Notes for 2.3.1

> New: When a KYC proposal is rejected, the reason for KYC rejection needs to be returned to the front end customer.app.KycWebApiService.checkKycApply
>
> Registration interface, when the gameplay asset is adjusted to non-mandatory, the current company's default account group gameplay asset is registered customer.app.CustomerWebApiService.register
>
> When adding a withdrawal address, you also need to perform security verification (regular verification) on the withdrawal address customer.app.CustomerWalletWebApiService.addWithdrawalAddressMFA
>
> Added a new withdrawal address list interface, grouped by currency, and filtered by currency customer.app.CustomerWalletWebApiService.withdrawalAddressGroupList
>
> Add a new withdrawal address list. You need to add whether the address is available (based on the address effective time) customer.app.CustomerWalletWebApiService.withdrawalAddressList
>
> Adjustment: Check the customer's withdrawal limit conditions fund.app.WithdrawAppDubboService.checkWithdrawRiskLimitConfig
>
> The withdrawal amount is not configured, and the withdrawal amount is not returned. fund.app.WithdrawAppDubboService.queryRemainWithdrawAmount
