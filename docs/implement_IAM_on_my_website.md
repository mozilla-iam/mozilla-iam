# Implement IAM (Single Sign On, API authorization, etc.) on my website

This document covers various options to implement IAM (Identity and Access Management) for your website.
These are the options Mozilla also currently utilize with what we call Mozilla IAM.

## I need a login system for my users

### Add this to my website!

You will have to choose an authentication protocol (ordered by preference):

- OIDC (Open ID Connect)
- SAML
- OAuth2 (without OIDC)
- WS Federation

The most common for open source apps and recent commercial applications is OIDC, while SAML is more common for enterprise-style applications or older applications. In some cases only OAuth2 is supported, and Windows-based services sometimes support WS Federation. Your mileage may vary.

In all cases you will need to (https://mana.mozilla.org/wiki/display/SECURITY/SSO+Request+Form)[register with us]. You will get a set of credentials in exchange, to setup your application.

#### Access proxies / Reverse proxies

For OIDC and SAML we recommend that you use a reverse proxy (also called Access Proxy). The proxy will front **all** inbound requests and perform authentication requests as well as authorization separately from your application. It's safer and it's easier to deploy and manage.

This is our default recommendation, if you can, you should use them!

The proxies will pass headers with the usernames, groups, information, etc. to your application that are easy to consume.

Examples of proxies:

- https://github.com/mozilla-iam/mozilla.oidc.accessproxy (General purpose reverse proxy utilizing Lua/OpenResty/NGINX, easily customizable)
- https://github.com/keycloak/keycloak-gatekeeper (Nice reverse proxy in Golang)
- https://github.com/zmartzone/mod_auth_openidc (OIDC Reverse proxy for Apache)
- https://cloud.google.com/iap/ (Great if you use GCP)
- https://aws.amazon.com/blogs/aws/built-in-authentication-in-alb/ (note: there are caveats with this solution at the time of writing this document - in particular it cannot filter access based on claims, so users are let in as long as they're able to authenticate. If that's an issue, use another proxy.)

#### Custom integration

It is possible to add OIDC or SAML support to your application yourself or utilizing a library. In doubt we recommend that you use an existing library. OIDC looks simple on the surface, but there are many caveats and hidden details that you will eventually run into. Remember that authentication bugs can up triggering severe incidents when these allow bypassing your access control layer.

If you do implement or customize implementation yourself, please have a look at our Infosec guidelines first:

- https://infosec.mozilla.org/guidelines/iam/openid_connect
- https://infosec.mozilla.org/guidelines/iam/saml.html

When using a library, this is a lesser problem as they normally take care of everything. Here's a few examples you can use:

- https://github.com/mozilla/mozilla-django-oidc/ (Python, Django, OIDC)
- https://www.npmjs.com/package/openid-client (NodeJS)
- https://docs.rs/oidc/0.2.0/oidc/ (Rust)
- https://auth0.com/docs/quickstart/backend/ (Auth0 examples)

### Can I add this to my desktop client / CLI?

For desktop clients, a common solution is to include a browser engine that will load a web page to authenticate. However, even when doing so there is a more elegant solution called PKCE (Proof Key for Code Exchange).

PKCE works for CLI (Command Line Interface) clients as well as desktop applications.

It works by sending a secret and unique challenge (proof key) through a `GET` parameter on a URL launching the user's local web browser (this can also show a QR code for a mobile device to load the page!), and getting an exchange code back from our access provider by pooling the access provider API with the secret and unique challenge (proof key).

The access provider knows when the user authenticated successfully for this proof key and will return a valid code. This allow for authentication to be performed without running a web-server. Some PKCE clients also run a local web server for convenience of implementation but it's not required (and should not be done if you plan on displaying a QR code for a mobile web browser to authenticate separately from the machine the client is running on).

- PKCE implementation documentation: https://auth0.com/docs/api-auth/tutorials/authorization-code-grant-pkce
- Example for Mercurial: https://github.com/mozilla-iam/federated-mercurial/

## I need to authorize an API for machines and/or single page apps (SPAs)

Our Access Provider is ultimately an OAuth2 Authorizer. What this means is that it functions as a ticket vending machine for OAuth2 access tokens and can front authentication with OIDC (or the SAML, WS Federation adapters), but also front your API.

When using this option, a user of your API authenticate/exchanges credentials for an access token with our Access Provider (Auth0) as such:

```
curl -X POST -H "Content-Type: application/json" https://auth.mozilla.auth0.com/oauth/token -d \
'{"audience":"api.sso.mozilla.com","scope":"classification:staff_confidential display:staff",\
"grant_type":"client_credentials","client_id": "YOUR CLIENT ID", "client_secret": "YOUR CLIENT SECRET"}'
```

In this case, `audience` is your API audience and can be anything that identifies your API. `scope` represent a set of permissions for your API. These scopes are customized by you, so you choose what they're called and what they do. Finally in this case it uses the `client_credentials` grant with a `client_id` and `client_secret` to identify the caller of the API. This is generally the case for machines calling APIs.

For SPAs calling APIs this is usually done with the implicit flow and the user is authenticated to your API by setting an `audience` value which includes the Access Provider and your own API audience at the same time. It does not include any `client_secret` and an access token is only returned if the user authenticates successfully.

In either case you will be returned at least an access token and it's `expires_in` expiration time. The access token is an opaque, signed string representing your API credentials.
You can then send them to your API (through an HTTP header: `Authorized: Bearer ...`) as such:

```
curl -H  "Authorization: Bearer YOUR_TOKEN_HERE" https://your.api.here/route/something
```

Your API will receive the query, extract the access token and send it back to our Access Provider for verification and getting more information. It will get back an `exp` expiration time, the list of `scopes` that are granted (so that you know which API routes should be authorized for this query) and of course if the token is valid. The token validation itself is performed by verifying the token signature is valid, but does not require an API call to the Access Provider.

If the access token is associated with a user and that user becomes invalid for any reason (blocked, deactivated, etc.) the access token will also be invalidated. Note that the access token is short lived and must be eventually renewed.

See also https://auth0.com/docs/quickstart/backend/python for an implementation example.
