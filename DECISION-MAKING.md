`Last update: 2019-01`

> **Modules**
>   * [UX (User Experience)](#ux-user-experience)
>   * [Django OIDC](#django-oidc)
>   * [CIS (Change Integration Service)](#cis-change-integration-service)
>   * [IAM User Profile](#iam-user-profile)
>   * [Access Provider](#access-provider)
>   * [SSO Dashboard](#sso-dashboard)
>   * [SSO Dashboard Configuration and Access Control Database](#sso-dashboard-configuration-and-access-control-database)
>   * [New Login Experience (NLX)](#new-login-experience-nlx)
>   * [DinoPark](#dinopark)
>   * [Legacy Mozillians.org (to be replaced by DinoPark and CIS)](#legacy-mozilliansorg-to-be-replaced-by-dinopark-and-cis)
>   * [Phonebook](#phonebook)
>   * [IAM Infrastructure](#iam-infrastructure)
>   * [OpenLDAP](#openldap)
>   * [DuoSecurity (2FA)](#duosecurity-2fa)


# _Mozilla IAM_ Modules Owners

This document list which team or people are **responsible for making decisions** by service or component (module) of _Mozilla IAM_. This is inspired by [Mozilla's Module System](https://wiki.mozilla.org/Modules). This list is useful to expedite decisions. It does not mean that a module owner is the sole authority for the module, but it is the "go-to" person. In the module owner absence, module peers may also make decisions on behalf of the module owner.

All decisions are taken by consulting various parties of different teams in and outside of Mozilla.

**Module owners are responsible for:**

- Aligning module-level key results (KRs) with the IAM roadmap milestones and objectives. The IAM roadmap milestones are set together with the module owners the IAM product owner.
- Breaking down tasks associated with Objectives and Key Results into sub tasks that can be worked on in a sprint
- Making decisions about the module that align with OKRs and technical considerations
- Raising issues associated with OKRs, milestones, tech stack etc to IAM stakeholders

## Stakeholders

Stakeholders are high-level responsible, accountable persons for specific Mozilla functions. They're responsible for drafting the high-level OKRs, roadmap and resolving issues or problems.

* Open Innovation: @hmitsch
* Enterprise Information Security: @jeffbryner (Capability owner)
* IAM Product owner: @gdestuynder (Technical Lead)
* Program Manager: @waltschak

## UX (User Experience)

User flow, design, etc.

- Module Owner: @mbranson
- Peers: Rina

## Django OIDC

A Python Django module providing OpenID Connect (OIDC) support for relying parties, used by multiple sites.

- Module Owner: @johngian
- Peers: @akatsoulas

Repositories:
- https://github.com/mozilla/mozilla-django-oidc/

## CIS (Change Integration Service)

Backend which deals with IAM data integration from multiple sources and provides various APIs to CIS (PersonAPI, Change/Person endpoints, well-known endpoint). This includes signing, authorization, profile storage model, publishing code and drivers.

- Module Owner: @andrewkrug
- Peers: @gdestuynder @fiji-flo
- Operator: EIS

Repositories:
- https://github.com/mozilla-iam/cis
- https://github.com/mozilla-iam/cis_functions
- https://github.com/mozilla-iam/person-api
- https://github.com/mozilla-iam/gsuite-community-drive-driver
- https://github.com/mozilla-iam/slack-driver/


## IAM User Profile

The IAM user profile utilize by CIS and other modules. It also presents the schema and profile rules on the well-known endpoints.

- Module Owner: @gdestuynder
- Peers: @andrewkrug @fiji-flo
- Operator: EIS

## Access Provider

Provides OIDC, SAML, WS-FED, etc. connectivity and IdP shadowing for the purpose of providing identity and access management to relying parties. Currently utilizes Auth0 to perform this function. This includes all auth0 related CI, configuration and rule engine.

- Module Owner: @gdestuynder
- Peers: @jdow @gene1wood @andrewkrug
- Operator: Third party (Auth0)

Repositories:
- https://github.com/mozilla-iam/auth0-ci/
- https://github.com/mozilla-iam/auth0-deploy
- https://github.com/mozilla-iam/authzerolib

## SSO Dashboard

This is the application launcher available at https://sso.mozilla.com.

- Owner: @andrewkrug
- Peers: @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard

## SSO Dashboard Configuration and Access Control Database

This is the configuration and `apps.yml`.

- Owner: @jdow
- Peers: @andrewkrug @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard-configuration

## New Login Experience (NLX)

This is the login window for _Mozilla IAM_.

- Owner: @hidde
- Peers: @andrewkrug @gdestuynder @gene1wood
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/auth0-custom-lock

## DinoPark

This is the new place to edit _Mozilla IAM_ profiles, manage groups, search & discover people. It will be available at https://people.mozilla.org (beta at https://people.allizom.community).

- Owner: @fiji-flo
- Peers: @hidde @Gregoor @hmitsch
- Operator: ParSys

Repositories:
- https://github.com/mozilla-iam/dino-park-front-end
- https://github.com/mozilla-iam/dino-park-search
- https://github.com/mozilla-iam/dino-tree
- https://github.com/mozilla/mozillians

## Legacy Mozillians.org (to be replaced by DinoPark and CIS)

This is the place to edit _Mozilla IAM_ profiles, manage groups, search & discover people. It is available at https://mozillians.org.

- Owner: @hmitsch
- Peers: @johngian @akatsoulas @fiji-flo
- Operator: ParSys

Repository:
- https://github.com/mozilla/mozillians

## Phonebook

This is the Staff-only accessible system to access Mozilla's org chart and Staff profiles, available at https://phonebook.mozilla.org.

- Owner: @andrewkrug
- Peers: @atoll
- Operator: IT

Repository:
- https://github.com/mozilla/phonebook

## IAM Infrastructure

- Owner: @adelbarrio 
- Peers: @ziegeer @andrewkrug @fiji-flo
- Operator: EIS, SREs

## OpenLDAP

This is the Staff user database, credential storage and group system (IdP). It also contains some non-staff contributors.

- Owner: @jdow
- Peers: @gcox @gdestuynder
- Operator: EIS

## DuoSecurity (2FA)

This is the 2FA/MFA product utilized to augment OpenLDAP with a second-factor.

- Owner: @gdestuynder
- Peers: @jeffbryner
- Operator: Third party (Duo)
