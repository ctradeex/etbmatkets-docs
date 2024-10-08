# Readme

The user's third-party system is integrated with the account system of MulitMarket's white-label customers. Quick login to the third-party system is performed based on MulitMarket's white-label account system. To use this API, you need to apply for authorization information such as appid from the white-label customer.



## Process

Get the authorization code by jumping to the white label client page. The white label client requires the user to authorize the third-party system to obtain the authorization code. After the customer agrees, the code is returned to the third-party platform. The third-party platform obtains a valid access token for accessing user information by calling the backend interface based on the appId, appSecret, and code information. Finally, the basic user information can be obtained based on this token and authorization binding can be performed.&#x20;



## Steps:

1、Open the authorization page to obtain the authorization code \
https://www.headline.net/en-US/auth2/code?appId=088b591f5fd735be62608a272f4d971f\&thirdAppType=HG\&url=https%3A%2F%2Fwww.hg.com%2Flogin \
\
After the above authorization is confirmed, you will be redirected to \
https://www.hg.com/login?code=\*\*\*\*\*\*\*\*\&app=headline



2、The third-party platform exchanges the access token through the authorization code. By obtaining the code, the backend calls the interface to exchange for accessToken

\
3、Obtain user information based on the access token to bind the account. The backend of the third-party platform obtains user information based on the accessToken
