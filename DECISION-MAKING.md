`Last update: 2018-07`

# _Mozilla IAM_ Modules Owners

This document list which team or people are **responsible for making decisions** by service or component (module) of _Mozilla IAM_. This is inspired by [Mozilla's Module System](https://wiki.mozilla.org/Modules). This list is useful to expedite decisions. It does not mean that a module owner is the sole authority for the module, but it is the "go-to" person. In the module owner absence, module peers may also make decisions on behalf of the module owner.

All decisions are taken by consulting various parties of different teams in and outside of Mozilla.

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

Backend which deals with IAM data integration from multiple sources.

- Module Owner: @akrug
- Peers: @gdestuynder
- Operator: EIS

Repositories:
- https://github.com/mozilla-iam/cis
- https://github.com/mozilla-iam/cis_functions

## Person API

API which presents and allows manipulation of CIS data. This includes a publicly available endpoint to _Mozilla IAM_ (replacing the Mozillians.org API).

- Owner: @akrug
- Peers: @gdestuynder <can we add a ParSys Peer?>
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/person-api

## SSO Dashboard

This is the application launcher available at https://sso.mozilla.com.

- Owner: @akrug
- Peers: @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard

## SSO Dashboard Configuration and Access Control Database

This is the configuration and `apps.yml`.

- Owner: @jdow
- Peers: @akrug @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard-configuration

## GSuite Community Driver

This is the G Suite Team Drive integration.

- Owner: @akrug
- Peers: @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/gsuite-community-drive-driver

## Slack Driver

This is the driver for Slack user deprovisioning.

- Owner: @gdestuynder
- Peers: @akrug
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/slack-driver/

## New Login Experience (NLX)

This is the login window for _Mozilla IAM_.

- Owner: @hidde
- Peers: @akrug @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/auth0-custom-lock

## Mozillians.org Profile and Group Management

This is the place to edit _Mozilla IAM_ profiles, manage groups, search & discover people. It is available at https://mozillians.org.

- Owner: @hmitsch
- Peers: @johngian @akatsoulas @fiji-flo
- Operator: ParSys

Repository:
- https://github.com/mozilla/mozillians

## Phonebook

This is the Staff-only accessible system to access Mozilla's org chart and Staff profiles, available at https://phonebook.mozilla.org.

- Owner: @akrug
- Peers: @atoll
- Operator: IT

Repository:
- https://github.com/mozilla/phonebook

## IAM Infrastructure

- Owner (accountable, decision maker): TBD
- Peers: @danielh (infra) @adelbarrio (monitoring&alerting) @akrug @johngian
- Operator (responsible, developer): IT (MOC?)

Repository:
- TBD (infrastructure)
- TBD (monitoring&alerting)

## OpenLDAP

This is the Staff user database, credential storage and group system (IdP). It also contains some non-staff contributors.

- Owner: @jdow
- Peers: TBD
- Operator: EIS

## DuoSecurity (2FA)

This is the 2FA/MFA product utilized to augment OpenLDAP with a second-factor.

- Owner: @gdestuynder
- Peers: @jeffbryner
- Operator: Third party (Duo)
