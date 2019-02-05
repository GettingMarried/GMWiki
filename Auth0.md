# Auth0 Authentication and Authorization

Prezola have an Enterprise contract for multi tenant AaaS with Auth0. www.auth0.com

## Use Cases

### Application Login
Primary use case is for identity management and authentication of users both in current GM and the new GM application. Both applications will make use of Universal Login features in Auth0 which provides a hosted sign up and sign in page and incorporates the forgotten password trigger. 
One Universal Login hosted page is configured per tenant in Auth0.
Universal Login typically (enforced by the PHP SDK) allows for logging into the primary application as this is the specified Audience and the Scope requested is typically `id_token token`. This allows for an identity and access tokens to be returned from the Universal Login and persisted in the users session as required. The access token returned for the default `audience` and `scopes` is not useful for accessing APIs, see section below for securing APIs and use of Universal Login to do it.
[Universal Login](https://auth0.com/docs/hosted-pages/login)

### AuthZ for APIs
[Always Secure APIs with Access Token](https://auth0.com/docs/api-auth/why-use-access-tokens-to-secure-apis)

Public APIs in GM applications can be protected from unauthorised use by securing them with Auth0. We have use cases for Machine to Machine applications ([Machine to Machine App](https://auth0.com/docs/applications/machine-to-machine)) which use APIs for communication ([M2M Flow](https://auth0.com/docs/flows/concepts/m2m-flow)).

For securing publicly available APIs which are designed only for internal use (FE React App talks to our BE) we can use the same flow to get an Access Token for the FE app to use which identifies the app as the user but does *not* identify the logged in user of the app. We can provide the JWT style access token to the FE as part of the initialised state and have the app store the token for calls to the backend API(s).

Alternatively to have an access token which identifies the logged in user it is necessary to request the required scopes for the audience (API identifier). ~~This could cause a slightly disjointed experience as we would send the user to the `authorize` when they have already logged in and is not easily achieved with the Auth0 PHP SDK as "login" is assumed to be only used for the audience of the `userinfo` endpoint which allows for use that endpoint but doesn't give access to any other application.~~

~~The correct flow (Authorization Code Flow) to use is here: https://auth0.com/docs/flows/guides/regular-web-app-login-flow/call-api-using-regular-web-app-login-flow. The disjointed UX *should* be mitigated by the below statement.~~

> By default, Auth0 skips user consent for first-party applications, which are applications that are registered under the same Auth0 domain as the API they are calling; however, you can configure your API in Auth0 to require user consent from first-party applications. Third-party applications, which are external applications, require user consent.

Universal Login allows us to specify an `audience` for the API and the additional `audience` of the `/userinfo` endpoint is added. The `scopes` can then include the standard OIDC `id_token profile` and the `scopes` required for our APIs e.g. `read:website write:website`.
A [prototype](https://github.com/AmpersandHQ/gm-auth-proto) of this in operation has been made.
Ensure the correct format for the returned Access Token is given by following guidelines [here](https://auth0.com/docs/tokens/set-access-token-format).