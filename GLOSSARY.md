# IAM Glossary

## 2FA / MFA

2-Factor Authentication / Multi-Factor authentication. 

## Account Verification

When a user adds an account to Mozillians, they are asked to log in with that account so that we can verify that it is their account.

## Auto-login

NLX reattempting login with the user's last used (and stored) connection method.

## Auth0 Rules

Rules that we write that allow or disallow certain login behaviours with Auth0, for example: 

## Connection

What Auth0 calls identity providers.

## Identity Provider (IdP)

A service that people can use to log in with, for example Mozilla LDAP, Firefox Accounts, GitHub, Google. More generally: a server that provides identify information to other servers. 

Within Auth0, this is called ‘Connection’. 

## IdP Ratcheting

The process of, when someone uses an IdP that is more secure than the one they currently log in with, forcing that login method to be their main method. This ensures users always use the most secure method.

## NLX

The New Login Experience, Mozilla's custom Auth0 login form.

## OIDC

OpenID Connect, one of the main standards for authentication on the web, which lets users have one login to multiple sites. It is a layer on top of OAuth2.

## Person API

Our own API that returns Mozilla IAM profile information.

## Relying Party (RP)

A website / app people can log in to using Mozilla IAM, for example Moderator, SSO Dashboard, Discourse, Expensify.