`Last update: 2018-07`

# Service owners

High level service and product owners for Mozilla IAM.

* Capability owner: @jeffbryner
  * Product owner: @gdestuynder
    * Auth0 & Auth0 Lock & Auth0 Dashboard: @jdow @akrug @gdestuynder
    * Service Integration (CIS): @akrug
    * LDAP: @jdow
    * DuoSecurity: @gdestuynder
    * Mozillians.org: @hmitsch
    * WorkDay: HRIS

## Architects

* @gdestuynder (IAM, Security)
* @mvk-mozilla (IT)

## Program Managers

* @hmitsch

## User Experience (UX)

* @mbranson

# Modules owners

This document list which team or persons are responsible for which component (module) of the Mozilla IAM stack. This is
a more detailed model.

This is mainly useful for decision making and is loosely following the [Firefox Module
system](https://wiki.mozilla.org/Modules).

- **Owner**: A single person which is accountable for the module and normally the final decision maker. In case there is
  serious disagreement, the Service owner, Product owner, or Capability owner can still be consulted. The Capability
  owner has final say on all decisions.
- **Peers**: List of persons which can act on behalf of the Owner, in case the owner is unavailable.
- **Operator**: A single person or team which is responsible for keeping the system running, generally also the
  developer in a devops model.

## CIS (Change Integration Service)

Backend which deals with IAM data integration from multiple sources.

- Owner (accountable, decision maker): @akrug
- Peers: @gdestuynder
- Operator (responsible, developer): EIS

Repositories:
- https://github.com/mozilla-iam/cis
- https://github.com/mozilla-iam/cis_functions

## Person API

API which presents and allow manipulation of CIS data.

- Owner (accountable, decision maker): @akrug
- Peers: @gdestuynder
- Operator (responsible, developer): EIS


Repository:
- https://github.com/mozilla-iam/person-api

## SSO Dashboard

This is https://sso.mozilla.com

- Owner (accountable, decision maker): @akrug
- Peers: @gdestuynder
- Operator (responsible, developer): EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard

## SSO Dashboard configuration and access control database

This is the configuration and `apps.yml`.

- Owner (accountable, decision maker): @jdow
- Peers: @akrug @gdestuynder
- Operator (responsible, developer): EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard-configuration

## GSuite Community Driver

This is the team drive integration.

- Owner (accountable, decision maker): @akrug
- Peers: @gdestuynder
- Operator (responsible, developer): EIS

Repository:
- https://github.com/mozilla-iam/gsuite-community-drive-driver

## Slack Driver

This is the Slack deprovisioning driver.

- Owner (accountable, decision maker): @gdestuynder
- Peers: @akrug
- Operator (responsible, developer): EIS

Repository:
- https://github.com/mozilla-iam/slack-driver/

## New Login Experience (NLX)

This is the login window for Mozilla IAM.

- Owner (accountable, decision maker): @hidde
- Peers: @akrug @gdestuynder
- Operator (responsible, developer): EIS

Repository:
- https://github.com/mozilla-iam/auth0-custom-lock

## Mozillians.org profile editor

This is https://www.mozillians.org which manages profiles, groups, etc.

- Owner (accountable, decision maker): @hmitsch
- Peers: @johngian @akatsoulas @fiji-flo
- Operator (responsible, developer): Parsys

Repository:
- https://github.com/mozilla/mozillians

## Phonebook

This is https://phonebook.mozilla.org

- Owner (accountable, decision maker): @akrug
- Peers: @atoll
- Operator (responsible, developer): IT

Repository:
- https://github.com/mozilla/phonebook
