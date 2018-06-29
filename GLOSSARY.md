# IAM Glossary

## 2FA (2 factor authentication) / MFA (Multi-factor Authentication)

Multi-factor authentication (MFA) is a security system that requires more than one method of authentication from independent categories of credentials to verify the user's identity for a login or other transaction.  See also the [Infosec website](https://infosec.mozilla.org/fundamentals/rationales.html#mfa)

## Account Verification

Account verification is a mechanism that verifies that a user account on another property belongs to the same user. It is not a login mechanism. Ex: a user may verify their Bugzilla account and add this information to their Mozilla IAM profile. It will require them to authenticate with Bugzilla in order to prove ownership of the Bugzilla account. This fact will be recorded.

The current account verification mechanism is provided by <https://www.mozillians.org>.

## Relying Party

Relying Party, or RP in short, is the property a user accesses after being authenticated. For example <http://discourse.mozilla.org/> is a relying party. It relies on the authentication provider to perform user authentication.

## SSO (Single Sign On)

Single Sign On is a generic term which indicates that a single authentication provider handles all authentication tasks for relying parties. As a user, it means that you can use a single account and login a single time to access a variety of relying parties. Ex: login to <http://discourse.mozilla.org/>  using SSO, then access <https://www.mozillians.org> without being required to login again or create a new account as they both support and use the same SSO.

## NLX (New Login Experience)

New Login Experience is a codename for the login screen of Mozilla IAM. It is also sometimes called the login window and the lock for historical reasons.

## Auto-login

This is generally known as the "remember-me" feature. It is a mechanism that will attempt to automatically log a user to a relying party in if their SSO session is still active and valid.

[NLX](https://github.com/mozilla-iam/auth0-custom-lock) supports auto-login by storing the user's last used connection method.

## Identity Provider (IdP)

The Identity Provider, or IdP, is a service that holds the source of truth of specific user identity information, and in particular, their password or authentication credentials. Ex: Mozilla LDAP, Firefox Accounts, GitHub, Google.

## Login Ratcheting

When a user logs in Mozilla IAM, the user is forced to use a login method that is the most secure for their account's primary email.
Because Mozilla IAM may only be aware of more secure methods being available for that user over time, we call it racheting.

Ex: User first login with "passwordless" authentication (least secure) with email `xxx@example.net`. The user then later login with Firefox Accounts /w 2FA enabled as `xxx@example.net` which is more secure. Because both use the same (primary) email, Mozilla IAM will rachete the login, i.e. force the user to login with Firefox Account for every subsequent attempt.


## Open ID Connect (OIDC)

OpenID Connect, one of the main standards for authentication on the web. It is a layer on top of OAuth2. See also the [Infosec website](https://infosec.mozilla.org/guidelines/iam/openid_connect) for more information.

## Change Integration Service (CIS)

The Change Integration Service is the service that integrates IAM identity and access information from multiple IdPs into a single database.

## Person API

Person API is the API in front of CIS. It allows access to the user profile data, access information, etc. for other services.

## Auth0 specific vocabulary

### Rules

Rules that we write that allow or disallow certain login behaviours with Auth0, for example: 

### Connection

This is the Auth0 name for IdPs (Identity Providers).

### Clients

This is the Auth0 name for RPs (Relying Parties).

### Hosted Lock

This is the Auth0 name for NLX, when hosted by Auth0.
