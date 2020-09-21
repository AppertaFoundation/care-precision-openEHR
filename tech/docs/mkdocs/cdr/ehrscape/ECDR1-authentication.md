# Getting started - Authentication

Let's get started by hooking up to an openEHR CDR via the Better Ehrscape API. 

This API is supported by Better (along with the openEHR REST API) and Ripple Ethercis.

 We have included examples for the Better CDR used by the Apperta Code4Health platform.

## Authentication

All of the openEHR CDR API calls require some sort of authentication in the header. In production this is likely to be something like `JSON Web Tokens` (JWT) but for demo purposes both ehrBase and betterCDR support `Basic Auth` based on a Username and Password.


### Basic Authentication

If you have a Postman environment file related to your CDR, you should be able to find the Username and Password, and possibly the Basic Auth token, pre-calculated.

If it is not pre-calculated, it is easy to do so with code like this in javascript.

```js
 const authString = btoa(`${username}:${password}`)
 const authToken = `Basic: ${authString}`
        
```

You then need to send that token in the Authorization header of your REST call e.g. 

```bash
curl --location --request GET 'https://cdr.code4health.org/rest/v1/template' \
--header 'Accept: application/json' \
--header 'Authorization: {{authToken}}'
```


## Connecting to the CDR


To test our basic connection to the CDR, we will perform a very simple `List templates` call to list the openEHR templates currently registered with the CDR -> [Working with openEHR Templates](ECDR2-openehr-templates.md)
