`Last update: 2018-07`

# _Mozilla IAM_ Modules Owners

This document list which team or people are responsible for making decision by service or component (module) of _Mozilla IAM_. This is inspired by [Mozilla's Module System](https://wiki.mozilla.org/Modules).

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
