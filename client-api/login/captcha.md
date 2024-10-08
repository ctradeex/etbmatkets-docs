---
description: Captcha
---

# Captcha

In terms of interface security control, human-machine verification can play a key protective role, especially in complex network environments, to ensure system security and data integrity. The following method provides how to access human-machine verification in the MultiMarket system:

## Verification access

> This function is connected to Google's official reCAPTCHA, [https://developers.google.com/recaptcha](https://developers.google.com/recaptcha)

## Involved interfaces

login/customer.app.CustomerWebApiService.login global/message.app.VerificationApiService.verifyCodeSend register/customer.app.CustomerWebApiService.register

```
headrs: {
// Add google captcha to request header
captcha: zxksjkdjskdjsd
}
```

## Access steps

> For detailed access documents, see: [https://developers.google.com/recaptcha/docs/display](https://developers.google.com/recaptcha/docs/display)

### Register Google reCAPTCHA and get the key

* Register a new website in the management platform http://www.google.com/recaptcha/admin, fill in the form and select the reCAPTCHA version (v2 or v3) suitable for your website
* After completing the registration, you will get a "Site Key" and a "Secret Key". The site key is used for the front-end, and the secret key is used for back-end verification.

### Front-end page integration (V3 version) Official example:

1. Add the following code to your HTML page, usually in the tag

```
<script src="https://www.google.com/recaptcha/api.js?render=your_site_key"></script>
```

Replace your\_site\_key with the site key you obtained in the Admin console.

2. According to the needs, when the user submits the form (login, registration, get verification code, etc.), call the grecaptcha.execute method to obtain the parameters required for the interface request `captcha`

```
<script>
function onClick(e) {
e.preventDefault();
grecaptcha.ready(function() {
grecaptcha.execute('reCAPTCHA_site_key', {action: 'submit'}).then(function(token) {
// Add your logic to submit to your backend server here.
});
});
}
</script>
```

3. Add the request header when requesting the interface and pass it to the backend for verification

```
headrs: {
// Add google captcha to the request header
captcha: zxksjkdjskdjsd
}
```

4. Initiate an interface request Pass verification: Request content is returned normally Failed: `{"msg":"Illegal request parameters","code":"F999999","bizCode":"G"}`

### Front-end Vue integration (V3 version) Example:

1. Download and import vue-recaptcha-v3

```javascript
npm i vue-recaptcha-v3 --save
// main.js
import { VueReCaptcha } from 'vue-recaptcha-v3'
app.use(VueReCaptcha, {
    // Replace with the site key you obtained in the management console
    siteKey: '6LcNvBUqAAAAABz2_ieWJEtdmyK_-oUUEk04Y1z4',
    loaderOptions: {
        // Due to restrictions in some countries, there is an option to enable the use 
        // of recaptcha.net instead of google.com.
        useRecaptchaNet: true
    }
}) 
```

2. Create the useRecaptcha.js file

````
import { useReCaptcha } from 'vue-recaptcha-v3'
import { reactive, onMounted, toRefs } from 'vue'
import { useStore } from 'vuex' export default function useRecaptcha () { const { executeRecaptcha: _executeRecaptcha, recaptchaLoaded } = useReCaptcha() const store = useStore() const state = reactive({ // SDK loading loading: false, // SDK loading completed loaded: false }) onMounted(async () => { try { state.loading = true // Initialize Google reCAPTCHA SDK const res = await recaptchaLoaded() if (res) { state.loaded = true } } catch (error) { console.log('🚀 ~ onMounted ~ error:', error) } finally { state.loading = false } }) // Get Google reCAPTCHA verification code const executeRecaptcha = async () => { try { const captcha = await _executeRecaptcha('verifyCodeSend')
await store.commit('_base/UPDATE_captcha', captcha)
return captcha
// Update global captcha data
} catch (error) {
console.log('🚀 ~ executeRecaptcha ~ error:', error)
}
}

return {
...toRefs(state),
executeRecaptcha,
recaptchaLoaded
}
}

```
3. Define captcha global data in vuex store
```
// src/store/modules/base.js
export default {
state: {
// Google human-machine verification captcha
captcha: ''
},
mutations: {
// Update Google human-machine verification captcha
UPDATE_captcha (state, data) {
state.captcha = data
},
}
}

```
4. Add error prompt to axios interceptor
```
service.interceptors.response.use(
response => {
const { data } = response
if (data.code === 'F999999') {
// Prompt text needs to be processed in multiple languages
Toast('Illegal request parameters')
return data
}
return response
},
error => {
return Promise.reject(error)
}
)
```
5. Usage example
```

/** Step 1: Introduce useRecaptcha hook **/
const { executeRecaptcha } = useRecaptcha()

/** Step 2: Add captcha parameter to the header of the verification code sending interface **/
// Send verification code
export function verifyCodeSendRequest (data) {
return request({
url: '/global/message.app.VerificationApiService.verifyCodeSend',
method: 'post',
headers: {
version: '0.0.1',
// Add Google verification code to request header
captcha: window.store.state._base.captcha
},
data
})
}

/** Step 3: Execute executeRecaptcha in front of the interface that needs to add captcha parameters **/

// Send verification code message.app.VerificationApiService.verifyCodeSend
const verifyCodeSend = async () =>{
await executeRecaptcha('verifyCodeSend')
await verifyCodeSendRequest()
}

// Login login/customer.app.CustomerWebApiService.login
const login= async () =>{
await executeRecaptcha('login')
await loginRequest()
}

// Registration interface: register/customer.app.CustomerWebApiService.register const register = async () =>{ await executeRecaptcha('register') await registerRequest() } ```
````
