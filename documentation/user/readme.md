# Authentication

Contact Blackstar for an account to be created for you. The account can be used in both PRODUCTION and UAT environments.

`Please note that your IP has to be whitelisted in PRODUCTION`

## Token management

You will get an access token that will be valid for 5 minutes. After the expiry of the access token, use the refresh token to get a new access token.

You can set up a middleware or interceptor that checks and refreshes your access token when a request is made.

`Note that refresh token expires in 90 days`

## Use

Pass the access token to the `Authorization` in the header

`Authorization: Bearer <ACCESS_TOKEN>`
