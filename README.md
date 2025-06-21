# WDV 4416 Postman Load Test Project

## To run project

```shell
npm i
npm start
```

Several tests initially failed due to improper handling of the authorization token. The profile endpoint requires a valid JWT token to access user information, but the tests did not save and reuse the token returned by the login request. This caused unauthorized errors and test failures.

To fix this, I added a script in the Login request's Tests tab to save the token into a collection variable using `pm.collectionVariables.set("token", jsonData.token);`. Then, I updated the Profile request's Authorization header to use `Bearer {{token}}`, which correctly passes the token with each Profile API call.

Additionally, I adjusted the Bad Token Profile test to expect a 401 Unauthorized response to validate the API’s security. This approach fixed the failing tests without changing the backend code or increasing delay times. Now, all tests run successfully in Postman.
